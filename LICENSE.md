<!doctype html>

<html>
  <head>
    <title>Get the coordinates on canvas</title>
    <meta charset="utf-8" />
   </head>

  <body>
    <canvas id="canvas"></canvas>
     <script type="text/javascript">
      
      var x = 2;
      var y = 2;
      var sx = 50;
      var sy = 50;
      var sx1 = 0;
      var sy1 = 0;
      var canvas = document.getElementById("canvas"),
      ctx = canvas.getContext('2d'), 
      pic = new Image();
      mount = new Image();  
      tree = new Image();           
      pic.src = 'grass.png'; 
      mount.src = 'mount.png';
      tree.src = 'tree.png';
      function move()
      {
        pic.onload = function() 
          { 
             for(var i = 0; i < canvas.height / sy; i++)
             {  
               for(var j = 0; j < canvas.width / sx; j++)
               {
                 ctx.drawImage(pic, sx1, sy1, sx, sy);
                 sx1 += sx;
               }
               sy1 += sy;
               sx1 = 0;
            }
         }
      }
      canvas.width  = 2000 - (2000 % sx);
      canvas.height = 2000 - (2000 % sy);  
      function mas( p, q ) 
      {
        return canvas.width / sx * p + canvas.height / sy * q;
      }
      var mass[canvas.width / sx * canvas.height / sy]
      for (var i = 0; i < (canvas.width / sx * canvas.height / sy); i++)
      {
        var mass[i] = 0;
      }
      console.log(mas);
      move();

      document.addEventListener("DOMContentLoaded", init, false);
      function init()
      {
        var canvas = document.getElementById("canvas");
        canvas.addEventListener("mousedown", getPosition, false);
      }

      function getPosition(event)
      {
        var x = new Number();
        var y = new Number();
        var canvas = document.getElementById("canvas");

        if (event.x != undefined && event.y != undefined)
        {
          x = event.x - 8;
          y = event.y - 8;
        }
        else 
        {
          x = event.clientX + document.body.scrollLeft +
              document.documentElement.scrollLeft;
          y = event.clientY + document.body.scrollTop +
              document.documentElement.scrollTop;
        }
        ctx.drawImage(mount, x - ((window.pageXOffset + x) % sx) + window.pageXOffset, y - ((y + window.pageYOffset) % sy) + window.pageYOffset, sx, sy);
      }
    </script>
  </body>
</html>
