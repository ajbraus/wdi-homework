# Bootstrap

What it is

## Key Questions

## UX & UI
  * UX = User Experience
  * UI = User Interface

#### Key Takeaways
  * UX encompasses all aspects of the end user's interaction, including product design, usability, and interface layout
  * UI refers to the visual elements (typography, buttons, forms, etc.)

#### Why is UX important?

  As developers, we want to make web applications that are *useable* and make people *happy*.

## Bootstrap
  * [Bootstrap Docs](http://getbootstrap.com/css)
  * CSS library developed by Twitter
  * Best known for responsive grid system

#### Why Use Bootstrap
  * Powerful tool for quickly implementing UX and responsive design
  * Enforces [semantic CSS class names](https://css-tricks.com/semantic-class-names)
  * Can be [minimal](http://dartjobs.herokuapp.com) or [customized](https://www.stitchfix.com)

#### How to Use Bootstrap
  * Add the the viewport meta tag and the [Bootstrap CDN](http://getbootstrap.com/getting-started/#download) to the `<head></head>` of your HTML file

  ```
  <head>
      <meta name="viewport" content="width=device-width, initial-scale=1">
      <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.5/css/bootstrap.min.css">
  </head>
  ```

  * You can also use this [Bootstrap boilerplate](https://github.com/sf-wdi-19-20/modules/tree/master/w1_d2_2_bootstrap_css/bootstrap_boilerplate) to get started

#### Bootstrap Grid System
  * `.container` class holds `.row` classes
  * Rows create horizontal groups of columns
  * Site content lives in columns

  ```
  <body>
      <div class="container">
        <div class="row">
          <div class="col-sm-6">
            <p>This column takes up half the page.</p>
          </div>
          <div class="col-sm-6">
            <p>And so does this one!</p>
          </div>
        </div>
      </div>
  </body>
  ```

  * Predefined column classes `col-*`
      * `xs-*`, `sm-*`, `md-*`, `lg-*` refer to [targeted device sizes](http://getbootstrap.com/css/#grid-media-queries)
      * Number between `1-12` sets width of `col` on that device and all larger devices


  * The best way to learn about the Boostrap grid system is to [see it in action](https://sf-wdi-19-20.github.io/modules/w1_d2_2_bootstrap_css/bootstrap_grid/index.html)
