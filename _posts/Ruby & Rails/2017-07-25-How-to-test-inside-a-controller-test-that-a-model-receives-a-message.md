---
layout: post
title: "How to test inside a controller test that a model receives a message"
description: ""
category: [rspec]
tags: []
---
{% include JB/setup %}

**The controller**

  def charge
    authorize(@order)
    stripe_token = params.require :stripe_token
    if @order.charge! stripe_token
      flash[:success] = t '.success'
      redirect_to my_reservations_orders_path
    else
      @order.reload # for cleaning up any possibly modified attributes
      flash[:error] = t 'stripe.payment_failed'
      redirect_to @order.payment_link
    end
  end

  def set_order
    @order = SpaceOrder.find_by(id: params[:order_id])
  end


**The controller test**

      describe '#charge!' do
      ....
           let(:stripe_token) { SecureRandom.hex }
           let(:order_params) {
              {
                id: order.space_id,
                order_id: order.id,
                stripe_token: stripe_token
              }
            }
            
            def the_action
              post :charge, order_params
            end
            

              describe "paying an open order I own" do
                let(:space)            { FactoryGirl.create :space, :fixed_price, billable_type, :approved }
                let(:order)             { FactoryGirl.create type, billable_type, :approved, user: user, space: space }

                  it "invokes Order#charge!", :aggregate_failures do
                    ensure_order_is_payable_and_user_owns_it(order, user)

                    # next line is necessary because the instance that is receiving the message 'charge!' is the new one created in the controller, not the creating in the test
                    expect(SpaceOrder).to receive(:find_by).with(id: order.id.to_s).and_return(order)
                    expect(order).to receive(:charge!).and_call_original
                    the_action
                  end

