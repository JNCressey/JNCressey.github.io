# Barcode sheet generator

My repo: [https://github.com/JNCressey/labels-print](https://github.com/JNCressey/labels-print)

## Intro

I made an HTML generator for a sheet of labels for printing on label paper.

There are two implementations, one using a single HTML file taking URL parameters, and one as a Google Apps Script web-app.

## Static Example

I have a static lorem ipsum example in this repo. This showcases the CSS required to arrange labels for a specific arrangement, but written in a way that can have the values easily swapped out to comply to other arrangements.

I have made it display gridlines when viewed on a screen to more easily preview what a page will look like. These lines are not printed.

[example link](https://jncressey.github.io/blogs/barcodes/example/static/labels-print-a4-avery-L7060--L7160-3x7-landscape.html)

## By URL Parameters

This dynamic example showcases the ability to prepare the inner html of a label, and have a sheet produced into the print arrangement. This implementation uses URL parameters to pass in the data and client-side JavaScript to build the page. This makes live example possible on GitHub Pages, since GitHub Pages has no option for server-side scripting.

[example link](https://jncressey.github.io/blogs/barcodes/example/url-param/labels-print-a4-avery-L7060--L7160-3x7-landscape.html?labelHTML=%09%09%3Cdiv%20style%3D%22%2F*background-color%3Ayellow*%2F%3Bheight%3A100%25%3Bwidth%3A100%25%3Bbox-sizing%3Aborder-box%3Bpadding%3A2mm%3Bdisplay%3Aflex%3Bflex-direction%3Acolumn%3B%22%3E%0A%09%09%09%3Cp%20style%3D%27width%3A100%25%3Btext-align%3Acenter%3Bmargin%3A0%3Bfont-family%3Asans-serif%27%3ELorem%20Ipsum%3C%2Fp%3E%0A%09%09%09%3Cdiv%20style%3D%22flex%3A1%201%20auto%3Btext-align%3Acenter%3Bmin-height%3A0%3B%22%3E%0A%09%09%09%09%3Cimg%20src%3D%22https%3A%2F%2Fjncressey.github.io%2Fblogs%2Fbarcodes%2Fexample%2Fassets%2F500x300-placeholder.png%22%20style%3D%22width%3A100%25%3Bheight%3A100%25%3Bobject-fit%3Acontain%22%3E%0A%09%09%09%3C%2Fdiv%3E%0A%09%09%3C%2Fdiv%3E)

## By Google Apps Script

The files within the Google Apps Script folder of my repo show an implementation written in google apps script as a web app deployment. Currently this only produces a lorem ipsum example, but can be modified from here for the functions to take arguments and produce bespoke output.

This implementation is better than relying on GitHub Pages because the label data isn't passed as URL parameters to my GitHub Page; instead, the document is prepared by the script itself. Therefore, it can be implemented securely within a self-contained ecosystem without sending data outside.

See the Google Apps Script files on my repo: [https://github.com/JNCressey/labels-print](https://github.com/JNCressey/labels-print)
