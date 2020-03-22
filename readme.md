# Fast way to get an iPhone X screen in Chrome Devtools

Thus "emulating" an iPhone X.

Source and cred: https://stackoverflow.com/questions/47552632/emulate-iphone-x-on-chrome

1. Paste the file iPhoneX.png to a folder where the local dev-server gets it's resources, e.g. path C:\CCShare\athena\kata-app\build\img\iPhoneX.png (the file can be gotten with path  https://i.stack.imgur.com/k5RNK.png as well but if the application has CSP-rules for img the resource is not loaded).

2. Paste this code into the console. When the window equals to the iPhone X device, the iPoneX.png image will be added and then be removed when changing the window size.


```
iPhoneX();

window.onresize = window.onorientationchange = function() {
    //Your other functions
    setTimeout(iPhoneX,100);
}

function iPhoneX() {
    if (window.innerWidth == 375 && window.innerHeight == 812) {
        if (!document.getElementById('iphone_layout')) {
            var img = document.createElement('img');
            img.id = 'iphone_layout';
            img.style.position = 'fixed';
            img.style.zIndex = 9999;
            img.style.pointerEvents = 'none';
            img.src = '/xg/kata/en/img/iPhoneX.png'
            document.body.insertBefore(img,document.body.children[0]);
        }
    } else if (document.getElementById('iphone_layout')) {
        document.body.removeChild(document.getElementById('iphone_layout'));
    }
}
```
