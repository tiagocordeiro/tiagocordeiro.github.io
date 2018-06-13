---
layout: page
title: Contato
tagline: Entre em contato
---

<style>
input[type=text], select {
    width: 100%;
    padding: 12px 20px;
    margin: 8px 0;
    display: inline-block;
    border: 1px solid #ccc;
    border-radius: 4px;
    box-sizing: border-box;
}

input[type=submit] {
    width: 100%;
    background-color: #4CAF50;
    color: white;
    padding: 14px 20px;
    margin: 8px 0;
    border: none;
    border-radius: 4px;
    cursor: pointer;
}

input[type=submit]:hover {
    background-color: #45a049;
}

div {
    border-radius: 5px;
    background-color: #f2f2f2;
    padding: 20px;
}
</style>

Envie sua mensagem

<form id="contactform" method="POST">
    <input type="text" name="name" placeholder="Seu nome">
    <input type="email" name="_replyto" placeholder="Seu email">
    <input type="hidden" name="_subject" value="Ferrablog contact" />
    <textarea name="message" placeholder="Sua mensagem"></textarea>
    <input type="text" name="_gotcha" style="display:none" />
    <input type="submit" value="Enviar">
</form>
<script>
    var contactform =  document.getElementById('contactform');
    contactform.setAttribute('action', '//formspree.io/' + 'tiago' + '@' + 'mulhergorila' + '.' + 'com');
</script>

Here listed some resources which provide  a saas service as a backend for forms (contact forms, hiring forms, etc.) to designers and developers like you:
1. [Formspree (also open source, free)](https://formspree.io/)
2. [FormKeep](https://formkeep.com/guides/contact-form-jekyll)
3. [Simple Form](https://getsimpleform.com/)

[Go to the Home Page]({{ site.url }}{{ site.baseurl }})
