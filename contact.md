---
layout: page
title: Contato
tagline: Entre em contato
---

Envie sua mensagem

<form id="contactform" method="POST">
    <input type="text" name="name" placeholder="Seu nome">
    <input type="email" name="_replyto" placeholder="Seu email">
    <input type="hidden" name="_subject" value="Ferrablog contact" />
    <textarea name="message" placeholder="Sua mensagem"></textarea>
    <input type="text" name="_gotcha" style="display:none" />
    <input class="btn" type="submit" value="Enviar">
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
