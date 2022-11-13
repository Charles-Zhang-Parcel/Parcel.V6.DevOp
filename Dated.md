# Dated Notes (Discussions)

## 20221112

We should keep that default console screen - useful for outputting some runtime information, just like Rhino.

For "canvas" transformation including translation and scaling, we should directly make use of View (hence view transform) instead of handling it ourselves - the only exception being the "infinite" canvas texture background.

(SFML) Per snippet below, the "view Center" is relative to/per/as in screenspace, that is, when we use `new Vector2f(0, 0)` instead, we are effectively saying the (0, 0) coordinate will be displayed at the center of the screen (at the moment it's at top left):

```c#
private static void Window_Resized(object sender, SFML.Window.SizeEventArgs e)
{
    var window = (sender as RenderWindow);
    var view = window.DefaultView;
    view.Size = new Vector2f(e.Width, e.Height);
    view.Center = new Vector2f(e.Width / 2, e.Height / 2); // This is the "default look"
    window.SetView(view);
}
```

[MagicOnion](https://github.com/Cysharp/MagicOnion) provides a typed interface for RPC, however the server depends on ASP.Net and requires .Net Core+ (while the client can target .Net framework). Both ASP.Net Core and MagicOnion (which is built on top of gRPC) have over-complicated API and we want to keep our code as "original" (meaning as clean, straightfoward and dependency-free as possible), and for our purpose of simple communication, we can easily achieve what we want with sockets.