---
tags:
  - Unity
  - Script
---
- Description
```html
<!DOCTYPE html>
<html lang="en-us">
  <head>
    <meta charset="utf-8">
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8">
    <title>Unity WebGL Player | {{{ PRODUCT_NAME }}}</title>
    <style>body { background-color: #333; }</style>
  </head>
  <body style="text-align: center">
    <canvas id="unity-canvas" width={{{ WIDTH }}} height={{{ HEIGHT }}} style="width: {{{ WIDTH }}}px; height: {{{ HEIGHT }}}px; background: {{{ BACKGROUND_FILENAME ? 'url(\'Build/' + BACKGROUND_FILENAME.replace(/'/g, '%27') + '\') center / cover' : BACKGROUND_COLOR }}}"></canvas>
    <br><input type="button" value="Send to Unity" onclick="SendToUnity();" />
    
    <script src="Build/{{{ LOADER_FILENAME }}}"></script>
    <script>
      var unityInstance = null;
      
      createUnityInstance(document.querySelector("#unity-canvas"), {
        dataUrl: "Build/{{{ DATA_FILENAME }}}",
        frameworkUrl: "Build/{{{ FRAMEWORK_FILENAME }}}",
        codeUrl: "Build/{{{ CODE_FILENAME }}}",
#if MEMORY_FILENAME
        memoryUrl: "Build/{{{ MEMORY_FILENAME }}}",
#endif
#if SYMBOLS_FILENAME
        symbolsUrl: "Build/{{{ SYMBOLS_FILENAME }}}",
#endif
        streamingAssetsUrl: "StreamingAssets",
        companyName: "{{{ COMPANY_NAME }}}",
        productName: "{{{ PRODUCT_NAME }}}",
        productVersion: "{{{ PRODUCT_VERSION }}}",
        // matchWebGLToCanvasSize: false, // Uncomment this to separately control WebGL canvas render size and DOM element size.
        // devicePixelRatio: 1, // Uncomment this to override low DPI rendering on high DPI displays.
      }).then((createdInstance) => {
        unityInstance = createdInstance;
      });
      
      function SendToUnity() {
        unityInstance.SendMessage("JSListener", "RespondToBrowser", "Hello from the browser!");
      }
    </script>
  </body>
</html>
```