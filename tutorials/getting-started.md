# Getting started

Set up a [base riso object](https://antiboredom.github.io/p5.riso/#riso) for each color you want to print with.  It's constructor can take 3 parameters, the color, width and height. When called with just the one parameter for color, it will default to the canvas width and height.
  
The color parameter can be a string that is the name of the [riso ink color](http://stencil.wiki/colors) you want to print with. So for example: yellow = Riso('yellow') will create an object that will be previewed on screen at the RGB values of that ink type.  
    
This example prepares an image with black and yellow layers:  

```javascript
let black;
let yellow;

function setup() {
  createCanvas(600, 600);
  black = new Riso('black');
  yellow = new Riso('yellow');
}
```
  
Now that we have an object setup for our black and yellow layers, we can draw graphic elements to each. This code is added to setup and draws an ellipse on the black and an overlapping ellipse on the yellow layer:  

```javascript
  background(255); //set the on screen background to be white

  black.fill(255); // set fill on the black layer to be fully opaque
  black.ellipse(200, height / 2, 300, 300); // draw ellipse on black layer

  yellow.fill(255);
  yellow.ellipse(400, height / 2, 300, 300);
  ```

But in the overlapping area of the ellipses we don't want both ink colors to print over the top of one another. We only want this area to have black ink and so we can use the [cutout()](https://antiboredom.github.io/p5.riso/#cutout) function to cut out the overlapping yellow from the black layer:  

```javascript
  black.cutout(yellow); // cut yellow out of black
```

Now let's add some text also using the cutout function. First let's create an object to contain the text:   

```javascript
  let textGraphic = createGraphics(width, height); //create graphics object
  textGraphic.fill(0); //make fill 0
  textGraphic.textStyle(BOLD); //style text
  textGraphic.textFont('Arial');
  textGraphic.textAlign(CENTER, CENTER); 
  textGraphic.textSize(20); 
  textGraphic.text('P5.RISO', width / 2 + 5, height / 2); //write the test 'P5.RISO' to the object

```
Now that we have the text we want to use, let's cut it out from the black layer:  

```javascript
  black.cutout(textGraphic); // cut text out of black

  drawRiso();
```

The second line above is the [drawRiso()](https://antiboredom.github.io/p5.riso/#drawRiso) function. This function will draw each layer onto the screen to show a preview of how your print will look. Ususally you'd call this from the end of setup or draw.   
  
Now we have finished writing our code in setup, the last thing to do is to use the [exportRiso()](https://antiboredom.github.io/p5.riso/#expRiso) function to export our color layers as greyscale images for printing. It's best to use this function within a mouseClicked() event function or in a keyTyped() event function so that it will only export your files when either of these events occurs.   
  
Under draw (which is empty). Let's add in a mouseClicked event function:  


```javascript
function mouseClicked() {
  exportRiso();
}
```

Now when the mouse is clicked, all of our print files will export as pngs. Each can be used to make a master on the printer.  


Here is the [complete code described in this example.](https://editor.p5js.org/brain/sketches/GpuJH1Zur)
