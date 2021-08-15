# Tabs with Image Overlay

This tab is my personal practice on JavaScript. Image overlay idea is inspired by this website: https://asana.com/ <br>

### JAVASCRIPT
```javascript
document.querySelectorAll('#button-container button').forEach(button => {

    button.addEventListener('click', function(e) {

        let whether = e.target.className;

        let imgUrl = `${whether}.jpg`;

        let currentImgOverlay = document.querySelector(`.img-overlay.${whether}`);

        let restImgOverlay = document.querySelectorAll(`.img-overlay:not(.${whether})`);


        if (!currentImgOverlay.classList.contains('show')) {

            restImgOverlay.forEach(overlay => {
                overlay.classList.remove('show');
            });

            currentImgOverlay.classList.add('show');

            setTimeout(() => {
                document.querySelector('#img-container').style.backgroundImage = `url(${imgUrl})`;
            }, 500);
            
        }

    });
});
```

### HTML
```html
<section>
    <div id="wrapper">
        <div id="button-container">
            <button class="sun">Sunny</button>
            <button class="rain">Rainy</button>
            <button class="snow">Snowy</button>
         </div>

        <div id="img-container" style="background-image: url('sun.jpg');">
            <div class="img-overlay sun show"></div>
            <div class="img-overlay rain"></div>
            <div class="img-overlay snow"></div>
        </div>
    </div>
</section>
```

### CSS
```css
#button-container {
    width: 20%;
    display: flex;
    flex-direction: column;
    padding-right: 80px;
}

#button-container button {
    background-color: #00bf9c;
    color: white;
    border: none;
    padding: 10px 30px;
    font-size: 24px;
    border-radius: 4px;
    line-height: 1.2;
    cursor: pointer;
}

#button-container button:not(:first-child) {
    margin-top: 20px;
}

#button-container .rain {
    background-color: #e8384f;
}

#button-container .snow {
    background-color: #fd9a00;
}

#img-container {
    width: 80%;
    border-radius: 10px;
    box-shadow: 0 2px 8px rgb(241 242 242 / 5%);
    background-size: cover;
    background-position: center;
    position: relative;
    overflow: hidden;
}

.img-overlay {
    position: absolute;
    content: "";
    width: 100%;
    left: -100%;
    height: 100%;
    border-radius: 10px;
}

.img-overlay.show {
    animation: overlay 1000ms cubic-bezier(0.075, 0.82, 0.165, 1) alternate;
    pointer-events: none;
}

.img-overlay.sun {
    background-color: #00bf9c;
}
.img-overlay.rain {
    background-color: #e8384f;
}
.img-overlay.snow {
    background-color: #fd9a00;
}

@keyframes overlay {
    0% { left: -100%; }
    50% { left: 0; }
    100% { left: 100%; }
}

```