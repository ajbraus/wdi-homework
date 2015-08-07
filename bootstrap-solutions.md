## Challenges
1. Create an `index.html` file and add the [Bootstrap CDN](http://getbootstrap.com/getting-started/#download) (or use the boilerplate template below) to get started

  ```html
  <!DOCTYPE html>
  <html>
  <head>
    <meta charset="utf-8">

    <!-- set viewport to device width to allow responsiveness -->
    <meta name="viewport" content="width=device-width, initial-scale=1">

    <!-- Bootstrap CDN -->
    <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.5/css/bootstrap.min.css">

    <!-- custom styles (always require after Bootstrap) -->
    <link rel="stylesheet" href="style.css">

    <title>Bootstrap Boilerplate</title>
  </head>
  <body>
    <div class="container">
      <div class="row">
        <div class="col-sm-6">
          <h1>col-sm-6</h1>
          <p>These columns take up half the page.</p>
        </div>
        <div class="col-sm-6">
          <h1>col-sm-6</h1>
          <p>And they take up the whole page on small devices.</p>
        </div>
      </div>
    </div>
  </body>
  </html>
  ```
2. Add one `.container`, one `.row`, and three `.col-*` classes (your columns can be any widths that add up to 12)
  ```html
  ...
    <div class="col-sm-4">
      <h1>col-sm-4</h1>
      <p>These columns take up 1/3 the page and the whole page on small devices.</p>
    </div>
    <div class="col-sm-4">
      <h1>col-sm-4</h1>
      <p>These columns take up 1/3 the page and the whole page on small devices.</p>
    </div>
    <div class="col-sm-4">
      <h1>col-sm-4</h1>
      <p>These columns take up 1/3 the page and the whole page on small devices.</p>
    </div>
  ...
  ```
3. Make these girds

| Mobile (xs) | Tablet (sm) | Laptop (md) | Desktop (lg) |
|:-- | :-- |:-- | :-- |:-- |
| 12/12 | 4/8 | 4/8 | 3/7 (offset-1) |

  ```html
  ...
    <div class="col-sm-4 col-lg-3 col-lg-offset-1">
      <h1>col-sm-4</h1>
      <p>These columns take up 1/3 the page and the whole page on small devices.</p>
    </div>
    <div class="col-sm-8 col-lg-7">
      <h1>col-sm-4</h1>
      <p>These columns take up 1/3 the page and the whole page on small devices.</p>
    </div>
  ...
  ```
3. Make these girds
  * Mobile (xs) - 3/9
  * Tablet (sm) - 4/8
  * Laptop (md) - 5/7
  * Desktop (lg) - 5/5 (offset-1)
  
4. Add content to your columns (`<h1>`, `<p>`, `<img>`, etc.)
5. Add some [buttons](http://getbootstrap.com/css/#buttons) (you can even put [icons](http://getbootstrap.com/components/#glyphicons) inside!)

## Stretch Challenges
1. Add a [nav bar](http://getbootstrap.com/components/#navbar) to the top of your page.
2. Add a [form](http://getbootstrap.com/css/#forms) to your page.
3. Visit [Bootsnipp](http://bootsnipp.com), and choose any element(s) from the gallery to add to your page. (**Hint:** You will have to add your own stylesheet if any extra CSS is required for the element(s) you choose)
