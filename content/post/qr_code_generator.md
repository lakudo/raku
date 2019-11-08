---
title: "QR Code Generator"
date: 2019-11-08
categories:
  - "Miscellaneous"
tags:
  - "QR"
---

I just use [qrious.js](https://github.com/neocotic/qrious) to implement a simple QR code generator.Please feel free to try online QR code generator to make your own QR codes. It supports four levels of error correction, you can choose the right size for your QR codes in the range of 100 to 1000 and click on a color swatch in the swatches panel to change the foreground and backgroud color.
<!--more-->

<style>
    main section {
        min-width: 250px;
        max-width: 50%;
        height: 100%;
        text-align: center;
    }
    main img {
        box-shadow: 0 0 10px 5px #666;
    }
    main form {
        padding: 25px 0 50px 0;
        text-align: left;
    }
    main textarea {
        display: flex;
        justify-content: center;
        align-items: center;
        box-shadow: 0 0 2px 1px #666;
    }
    main form input,
    main form select {
        margin: 0 auto; 
        width: 100%;
    }
    main form input:invalid {
        outline: 2px solid #f00;
        color: #f00;
    }
</style>
<center><img id="qrious"></center>
<form autocomplete="off">
 <b>value</b>
   <center>
   <textarea type="text" name="value" spellcheck="false" class="form-control" 
    style="width:100%; height:150px;" value="Entering a URL"
    onblur="if(this.value==''){ this.value='Entering a URL'; this.style.color='#BBB';}"
    onfocus="if(this.value=='Entering a URL'){ this.value=''; this.style.color='#000';}"
    style="color:#BBB;" >Entering a URL</textarea>
    </center>
    <b>size</b>
    <input type="number" name="size" placeholder="100" min="100" max="1000" value="250">
    <b>level</b>
    <select name="level">
        <option value="L">L - 7% damage</option>
        <option value="M">M - 15% damage</option>
        <option value="Q">Q - 25% damage</option>
        <option value="H">H - 30% damage</option>
    </select>
    <b>background</b>
    <input type="color" name="background" value="#ffffff">
    <b>foreground</b>
    <input type="color" name="foreground" value="#000000">
</form>

<script src="https://unpkg.com/qrious@2.3.0/dist/umd/qrious.js"></script>
<script>
    (function () {
        var $background = document.querySelector('main form [name="background"]')
        var $foreground = document.querySelector('main form [name="foreground"]')
        var $level = document.querySelector('main form [name="level"]')
        var $section = document.querySelector('main section')
        var $size = document.querySelector('main form [name="size"]')
        var $value = document.querySelector('main form [name="value"]')

        var qr = window.qr = new QRious({
            element: document.getElementById('qrious'),
            size: 250,
            value: 'Hi~'
        })
        $background.addEventListener('change', function () {
            qr.background = $background.value || null
        })
        $foreground.addEventListener('change', function () {
            qr.foreground = $foreground.value || null
        })
        $level.addEventListener('change', function () {
            qr.level = $level.value
        })
        $size.addEventListener('change', function () {
            if (!$size.validity.valid) {
                return
            }
            qr.size = $size.value || null
            $section.style.minWidth = qr.size + 'px'
        })

        $value.addEventListener('input', function () {
            qr.value = $value.value
        })
    })()
</script>
