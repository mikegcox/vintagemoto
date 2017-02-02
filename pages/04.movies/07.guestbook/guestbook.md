---
title: Guestbook

form:
    name: guestbook
    fields:

        - name: author
          label: Name
          placeholder: Enter your name
          autofocus: on
          autocomplete: on
          type: text
          validate:
            required: true

        - name: email
          label: Email
          placeholder: Enter your email address
          type: email
          validate:
            required: true

        - name: text
          label: Message
          placeholder: Enter your message
          type: textarea
          validate:
            required: true

        - name: date
          type: hidden
          process:
            fillWithCurrentDateTime: true

        - name: g-recaptcha-response
          label: Captcha
          type: captcha
          recatpcha_site_key: 6Ldx1AcUAAAAACcV4zlixzyJYw1aYi92XDRbIhJn
          recaptcha_not_validated: 'Captcha not valid!'
          validate:
            required: true
          process:
            ignore: true

    buttons:
        - type: submit
          value: Submit

    process:
        - email:
            subject: "[Site Guestbook] {{ form.value.name|e }}"
            body: "{% include 'forms/data.html.twig' %}"
        - captcha:
            recatpcha_secret: ej32uej3u2ijeiu32jeiu3jeuj32ui
        - save:
            filename: messages.yaml
            operation: 'add'
        - message: Thank you for writing your message!
---

### This is a guestbook