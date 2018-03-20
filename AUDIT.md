# Performance Matters week 1 audit
I performed all my tests using the 'Slow 3G' setting in the Google Chrome dev tools. I have created a seperate branch for each feature. The data below is an average of 5 test results for each feature. 
## Minify code
In order to reduce the size of the files I minified the CSS and Javascript.
### Results
fonts.css 1.2kb (2.03s) -> 1kb (2.03s)  - 0.0s 

bootstrap.css 142kb (7.42s) -> 114kb (6.66s) - 0.74s

docs.css 30kb (3.82s) -> 20kb (3.32s) - 0.5s

bootstrap.js 68.3kb (4.36s) -> 36kb (3.63s) - 0.73s

##### Total: 241,5kb (17,63s) -> 171kb (15,64s) - 1.99s
#### Before
![Before minify](https://raw.githubusercontent.com/hackshackshacks/performance-matters/master/audit_images/network_before_minify-code.png)

#### After
![Before minify](https://raw.githubusercontent.com/hackshackshacks/performance-matters/master/audit_images/network_after_minify-code.png)

## Font loading
To reduce loading time and to prevent blocking I moved the Google Fonts styles into my own. This way I was able to retrieve only useful characters. I also added the `font-display: swap` property, this will prevent blocking and render the new font when it's loaded.
### Results
fonts.css 1.2kb (2.03s) -> 3.8kb (2.24s) + 0.21s

sourcesanspro-regular.woff2 75kb (9.91s) -> 0kb (0s) -9.91s

sourcesanspro-light.woff2 74kb (11.73s) -> 0kb (0s) -11.73s

##### Total: 150.2kb (23.67s) -> 3.8kb (0.21s) - 23.46s
#### Before
![Before minify](https://raw.githubusercontent.com/hackshackshacks/performance-matters/master/audit_images/network_before_font-loading.png)

#### After
![Before minify](https://raw.githubusercontent.com/hackshackshacks/performance-matters/master/audit_images/network_after_font-loading.png)

## Async styles
In order to improve the critical render path added async stylesheets. This will prevent blocking and result in visible content earlier in the loading process.
### Results
First meaningful paint 5,810ms -> 1,230ms (-4,58s)

Performance score by Google Lighthouse 61 - 85

#### Before
![Before minify](https://raw.githubusercontent.com/hackshackshacks/performance-matters/master/audit_images/performance_before.png)

#### After
![Before minify](https://raw.githubusercontent.com/hackshackshacks/performance-matters/master/audit_images/performance_after-async-styles.png)

## Critical styles
To reduce the time until the page is usable I added the most critical styles in-line. This way the page doesnt need to load the whole stylesheet to show the first few components.

## Minify images
The website was loading larger images than necessary. I compressed the images using tinypng.com and converted the jpg files to png.
### Results
Images total size 729kb (75,98s) -> 94,4kb (24,33s) -634,6kb (-51,65s)
#### Before
![Before minify](https://raw.githubusercontent.com/hackshackshacks/performance-matters/master/audit_images/network_before_imagemin.png)

#### After
![Before minify](https://raw.githubusercontent.com/hackshackshacks/performance-matters/master/audit_images/network_after_imagemin.png)

## Conclusion
All features appear to have a positive effect on the app's speed. Further testing would have to point out the exact benefit as the sample size of 5 is pretty small.