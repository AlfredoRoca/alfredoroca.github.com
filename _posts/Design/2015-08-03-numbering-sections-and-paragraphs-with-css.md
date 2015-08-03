---
layout: post
title: "Numbering sections and paragraphs with CSS"
description: ""
category: [HTML, CSS]
tags: [index, numbering]
---
{% include JB/setup %}


http://codepen.io/AlfredoRoca/pen/bdmBxr
HTML

    <div class="legal_doc">
      <article>
        <h3>title 1</h3>
        <section>
          <p>Articles are numbered with letters</p>
          <p>... this section without number</p>
            <ul>
              <li>...</li>
              <li>...</li>
            </ul>
        </section>
      </article>
      <article>
        <h3>title 2</h3>
        <section>
          <h4>title 3</h4>
          <div>
            <p>...</p>
            <p>...</p>
            <p>...</p>
          </div>
        </section>
        <section>
            <h4>title 4</h4>
            <div>
              <p>...</p>
              <p class="sub-p">...</p>
          </div>
        </section>
      </article>
    </div>



SCSS

    .legal_doc {
      margin-bottom: 3em;
      counter-reset: counter-letter;
      article { 
        counter-increment: counter-letter; 
        counter-reset: counter-number;
        h3:before { 
          content: counter(counter-letter, upper-alpha) '. ';
        }
        section {
          counter-increment: counter-number;
          margin-left: 1em;
          margin-bottom: 2em;
          h4:before {
            content: counter(counter-number) '. ';
          }
          div {
            counter-reset: counter-subnumber;
            counter-reset: counter-subsubnumber;
            margin-left: 1em;
            > p {
              counter-increment: counter-subnumber;
            }
            > p:before {
              content: counter(counter-number) '.' counter(counter-subnumber) '. ';
            }
            > p.sub-p {
              counter-increment: counter-subsubnumber;
              margin-left: 1em;
            }
            > p.sub-p:before {
              content: counter(counter-subsubnumber) ') ';
            }
          }
        }
      }
    }

