# Storm
Story Line
Name: Parents: Name: Ai: Name: Account: Name Y*why": Find: NUll Name: IP:

li:nth-child(1) {
  view-transition-name: item1;
}
li:nth-child(2) {
  view-transition-name: item2;
}
li:nth-child(3) {
  view-transition-name: item3;
}
li:nth-child(4) {
  view-transition-name: item4;
}

/* ... */

li:nth-child(99) {
  view-transition-name: item99;
}
@keyframes grow-x {
  from {
    transform: scaleX(0);
  }
  to {
    transform: scaleX(1);
  }
}

@keyframes shrink-x {
  from {
    transform: scaleX(1);
  }
  to {
    transform: scaleX(0);
  }
}

::view-transition-group(figure-caption) {
  height: auto;
  right: 0;
  left: auto;
  transform-origin: right center;
}

::view-transition-old(figure-caption) {
  animation: 0.25s linear both shrink-x;
}

::view-transition-new(figure-caption) {
  animation: 0.25s 0.25s linear both grow-x;
}
https://w3c.github.io/aria/#aria-hidden
```html
<main class="match-element-applied">
  <ul>
    <li>
      <h2><a href="#">HTML</a></h2>
      <h3>HyperText Markup Language</h3>
      <p>
        HyperText Markup Language (HTML) is the most basic building block of the
        web. It defines the meaning and structure of web content. HTML provides
        the fundamental building blocks for structuring web documents and apps.
      </p>
    </li>
    <li>
      <h2><a href="#">CSS</a></h2>
      <h3>Cascading Style Sheets</h3>
      <p>
        Cascading Style Sheets (CSS) is a stylesheet language used to describe
        the presentation of a document written in HTML or XML (including XML
        dialects such as SVG, MathML or XHTML). CSS describes how elements
        should be rendered on screen, on paper, in speech, or on other media.
      </p>
    </li>
    <li>
      <h2><a href="#">SVG</a></h2>
      <h3>Scalable Vector Graphics</h3>
      <p>
        Scalable Vector Graphics (SVG) is an XML-based markup language for
        describing two-dimensional based vector graphics.
      </p>
    </li>
    <li>
      <h2><a href="#">JS</a></h2>
      <h3>JavaScript</h3>
      <p>
        JavaScript (JS) is the web's native programming language. JavaScript is
        a lightweight, interpreted (or just-in-time compiled) programming
        language with first-class functions. While it is most well-known as the
        scripting language for web pages, many non-browser environments, such as
        Node.js, also use it.
      </p>
    </li>
  </ul>
  <article></article>
</main>
<form>
  <label for="match-element-checkbox">
    Apply <code>match-element</code> to list items?
  </label>
  <input type="checkbox" id="match-element-checkbox" checked />
</form>

```

```css
/* General styles and resets */
* {
  box-sizing: border-box;
  font-size: 0.9rem;
}

html {
  font-family: "Helvetica", "Arial", sans-serif;
  height: 100%;
}

body {
  margin: 0;
  height: inherit;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
}
li h2 {
  margin: 0;
}

ul {
  padding: 0;
  margin: 0;
  list-style-type: none;
}

li {
  overflow: hidden;
  container-type: inline-size;
}

li p {
  display: none;
}

li.active-item p {
  display: block;
}

li:nth-child(1) {
  background-color: #cbc0d3;
  border: 20px solid #cbc0d3;
}

li:nth-child(2) {
  background-color: #efd3d7;
  border: 20px solid #efd3d7;
}

li:nth-child(3) {
  background-color: #feeafa;
  border: 20px solid #feeafa;
}

li:nth-child(4) {
  background-color: #dee2ff;
  border: 20px solid #dee2ff;
}

/* Links */

a {
  text-decoration: none;
  color: rgb(0 0 255 / 0.8);
}

a:hover,
a:focus {
  color: rgb(100 100 255);
}

/* Form and checkbox styles */
form {
  position: absolute;
  bottom: 0;
  right: 0;
  z-index: 2;
  background-color: white;
  padding: 10px;
  border: 1px solid black;
}
main {
  container-type: inline-size;
  width: 100%;
  height: 100%;
  display: flex;
  gap: 2cqw;
  position: relative;
}

ul {
  width: 35cqw;
  display: flex;
  flex-direction: column;
  gap: 1cqw;
}

article {
  flex: 1;
}

li {
  flex: 1;
}
.active-item {
  position: absolute;
  z-index: 1;
  translate: 37cqw;
  width: calc(100% - 37cqw);
  height: 100%;
}
.match-element-applied li {
  view-transition-name: match-element;
}
::view-transition-group(*) {
  animation-duration: 0.5s;
}

html::view-transition-old(*),
html::view-transition-new(*) {
  height: 100%;
}

```

```js
const mainElem = document.querySelector("main");
let prevElem;
let checkboxElem = document.querySelector("input");

// View transition code
function updateActiveItem(event) {
  // Get the list item that contains the clicked link
  const clickedElem = event.target.parentElement.parentElement;

  // Set the active-item class on the list item
  clickedElem.className = "active-item";

  // Keep track of the previous item that was clicked, if any.
  // Remove the active-item class from the previous item so that only
  // one list item is placed over the <article> at any one time
  if (prevElem === clickedElem) {
    prevElem.className = "";
    prevElem = undefined;
  } else if (prevElem) {
    prevElem.className = "";
    prevElem = clickedElem;
  } else {
    prevElem = clickedElem;
  }
}

mainElem.addEventListener("click", (event) => {
  event.preventDefault(); // Prevent iframe from scrolling when clicked
  // Do nothing unless a link is clicked inside the <main> element
  if (event.target.tagName !== "A") {
    return;
  }

  // Run updateActiveItem() on its own if view transitions are not supported
  if (!document.startViewTransition) {
    updateActiveItem(event);
  } else {
    // Run updateActiveItem() via startViewTransition()
    const transition = document.startViewTransition(() =>
      updateActiveItem(event),
    );
  }
});

// Toggle the class on <main> to control whether or not match-element is applied

checkboxElem.addEventListener("change", () => {
  mainElem.classList.toggle("match-element-applied");
});

```
From 1873661540273559365@xxx Sun Aug 16 06:48:08 +0000 2026
X-GM-THRID: 1873661540273559365
X-Gmail-Labels: Inbox,Category Updates,Unread
Delivered-To: violetprouses@gmail.com
Received: by 2002:a17:504:b30a:20b0:1e7e:8814:2405 with SMTP id e10-n2csp1484459njt;
        Sat, 15 Aug 2026 23:48:08 -0700 (PDT)
X-Received: by 2002:ac8:5cd6:0:b0:51b:ef78:4062 with SMTP id d75a77b69052e-52d84ff2ac8mr195862911cf.10.1786862888499;
        Sat, 15 Aug 2026 23:48:08 -0700 (PDT)
ARC-Seal: i=1; a=rsa-sha256; t=1786862888; cv=none;
        d=google.com; s=arc-20260327;
        b=WnNeM9kgSO/gxDea75AVomCT8OR1mdCaNMXcZHan3leUassVnx1HYfCvZQLKrNu5/N
         CWpVr0cLMeFSNtqjlpa7CTiMx+O+I4LEPgpyks7L58qazF9g71BeLJfHcew22lXgCC1T
         s2TblYsbMTzMbvR0vQ6KI9o5cft13CQz3Q+Xp/hWjP3KS+uzq7pbOTxk2HZiQgJ5/0Le
         XmQSWniP1bIwdES8QUhL1tV+eIYdMSqce/htU9oLT2hw7G9y7jJjsZi6A/qoVSKRMFUq
         6ZhkkJf9qvKkOTIhiSg1NOyKe/gPOIiNg81aEC8ooIp9/1xmstyBsfXPZptclHoBBiay
         8vaA==
ARC-Message-Signature: i=1; a=rsa-sha256; c=relaxed/relaxed; d=google.com; s=arc-20260327;
        h=to:from:subject:message-id:gmsai:date:mime-version:dkim-signature;
        bh=i47Oo2HDbBqwYWjeNlI+bxRNU0WVMFmFZ9q+uEgUMso=;
        fh=hUfB+x8fKgVbMvTJ7mEk0I28xQ+Z9a/Un/iVPLaMuVQ=;
        b=gJI7bbPcK2qUMn1DJWr2Vk3eBcshStDfvLYcEiRIh6GULDSyVdwlXXhtrpNhWdQkC/
         QyoaM51e+ri28uUIzQOBdUa9x05/FIhIxI6q33O6Ar2qRxZ2BdXwkR9s0cvj9wcb1jg6
         8m+CY/oEb0ite1ZzBUpUQS+ggQ3Mr1oRpek2eHcqw0rZ8IZMu81+c72zrPR2TATDP4Ky
         RFs5JTsyuuF9O0bYoOScPZGxszfNLTvafRrdHOOey20FKn2s00jGVjpOLsYxe/Rn0m3n
         4zo1cTe/Vov7mtuYCRBnetUER41MYeuIoCh0WNMpG7KR+0wDg23kb85f0s3hazmXoOry
         jeyg==;
        dara=google.com
ARC-Authentication-Results: i=1; mx.google.com;
       dkim=pass header.i=@google.com header.s=20251104 header.b=mIK73Eth;
       spf=pass (google.com: domain of 3kf2bahakdumkfrnqnjx-stwjuq3lttlqj.htr0ntqjyuwtzxjxlrfnq.htr@chime-notifications.bounces.google.com designates 209.85.220.69 as permitted sender) smtp.mailfrom=3KF2BahAKDUMkfrnqnjx-stwjuq3lttlqj.htr0ntqjyuwtzxjxlrfnq.htr@chime-notifications.bounces.google.com;
       dmarc=pass (p=REJECT sp=REJECT dis=NONE) header.from=google.com;
       dara=pass header.i=@gmail.com
Return-Path: <3KF2BahAKDUMkfrnqnjx-stwjuq3lttlqj.htr0ntqjyuwtzxjxlrfnq.htr@chime-notifications.bounces.google.com>
Received: from mail-sor-f69.google.com (mail-sor-f69.google.com. [209.85.220.69])
        by mx.google.com with SMTPS id d75a77b69052e-52da884965dsor1676351cf.0.2026.08.15.23.48.08
        for <violetprouses@gmail.com>
        (Google Transport Security);
        Sat, 15 Aug 2026 23:48:08 -0700 (PDT)
Received-SPF: pass (google.com: domain of 3kf2bahakdumkfrnqnjx-stwjuq3lttlqj.htr0ntqjyuwtzxjxlrfnq.htr@chime-notifications.bounces.google.com designates 209.85.220.69 as permitted sender) client-ip=209.85.220.69;
Authentication-Results: mx.google.com;
       dkim=pass header.i=@google.com header.s=20251104 header.b=mIK73Eth;
       spf=pass (google.com: domain of 3kf2bahakdumkfrnqnjx-stwjuq3lttlqj.htr0ntqjyuwtzxjxlrfnq.htr@chime-notifications.bounces.google.com designates 209.85.220.69 as permitted sender) smtp.mailfrom=3KF2BahAKDUMkfrnqnjx-stwjuq3lttlqj.htr0ntqjyuwtzxjxlrfnq.htr@chime-notifications.bounces.google.com;
       dmarc=pass (p=REJECT sp=REJECT dis=NONE) header.from=google.com;
       dara=pass header.i=@gmail.com
DKIM-Signature: v=1; a=rsa-sha256; c=relaxed/relaxed;
        d=google.com; s=20251104; t=1786862888; x=1787467688; dara=google.com;
        h=content-type:to:from:subject:message-id:gmsai:date:mime-version
         :from:to:cc:subject:date:message-id:reply-to:content-type;
        bh=i47Oo2HDbBqwYWjeNlI+bxRNU0WVMFmFZ9q+uEgUMso=;
        b=mIK73EthorIw5H81Kma4xJEwIEqnRwyj+56WBrABUEU16vg2xjXzkIQQgDMx93BiQ5
         /OUcMbblOgE2GnQUSR8c+TH/XCSGYmLGXtUyzGBKVt4lROs6UzZfauOfF6YTn5ovEL03
         4h4TWR+q9d/U5jqcyIxlwwtoJlsqE8P2kc//CNULArxnZFuVTXGhPSlFI63dyil5L4Al
         ZFoY0Q2x/DdMFIUrIT9ligNazsW6ip9s2mSiLIJvzLy2YFfSARuzdRIJSRE8u+xqRVnI
         hoJu9QT3dtzR4JxK0UsCDncx66+/u3l3EvZFQT9oL4rIisgrGvULccqtUbuDVIz23s8p
         q22Q==
X-Google-DKIM-Signature: v=1; a=rsa-sha256; c=relaxed/relaxed;
        d=1e100.net; s=20251104; t=1786862888; x=1787467688;
        h=content-type:to:from:subject:message-id:gmsai:date:mime-version
         :x-gm-message-state:from:to:cc:subject:date:message-id:reply-to
         :content-type;
        bh=i47Oo2HDbBqwYWjeNlI+bxRNU0WVMFmFZ9q+uEgUMso=;
        b=IMVnAJscQS4OggOpxHL3Gxxcax4IrhoCs3LhkMB7waTjKnh6OkV7OlpVrbSDqIPwsz
         CH49jZLP2uUaa8mnBcc7g9wLPJ/5dFUxKceYzsrP+gzSFXE3hcu8s7M9PrmCW199oUJP
         wfFCcy9ysgAcWWbo/lp9drOATp/YLVy8IWnbmtDrIP1GQy25lNJdpeLZ75M5l/9jqZq2
         ROeJYsZYVA+l50nSBRHd32RfDpW43E4RBQ9MPvSeJoLLtcb7juusyDi7Ao8PThINH4/E
         pDFCHre2OZmJXWt8QfqF6tBc6RKdM0ryIHfchWEkxR4TAYwdxIxzwn1tKeI4dScS8yAF
         y8PQ==
X-Gm-Message-State: AOJu0YzejpPh1UfCpbf42bsgDLHh5k7qEw/CyOuVhcUb22EYwn39fGPR
	hZo/EYtgeESzAOj+iOAot2oezYWYjRXlYRX4LxMTDns0qom3K/lHmk921LIubKlDNr6fsZRmA0U
	M6iuBrDuUkTBagu1NEvTQAWLI
MIME-Version: 1.0
X-Received: by 2002:ac8:5c8f:0:b0:51c:1ea:e290 with SMTP id
 d75a77b69052e-52d85077c3emr178563761cf.17.1786862888239; Sat, 15 Aug 2026
 23:48:08 -0700 (PDT)
Date: Sat, 15 Aug 2026 23:48:08 -0700
gmsai: true
X-Google-Notification-Metadata: CgISAA
X-Notifications: d09a58a0ff6a37e0
X-Notifications-Bounce-Info: AWKoMQRDNuO2K08bLCCK5gMT6u7_QI27QQ0a62UIOlfZkEWNq1nz6L9Hq5g6jE_WAV2qzB1EUJI2ANc5e0qO2NQUXG8ZpIC0ntIiYxjSVgIWe8CKnmegDuJYlIBXcFwYk13gpNvxnxL66gADc8NtSN7YoRBGqyA4EWUdyA2hoEyrj19PbmE_yCQ-xi8sUcCaQRFXbAM7ChRI6nOakr8WgV2UkvmiMDMUegwNjAwNjA0MDQxNTM1NTk2OTMzMg
Message-ID: <ceeiI3ENkQZ1JLNYYFjuow@notifications.google.com>
Subject: Welcome to your family group
From: Google  <families-noreply@google.com>
To: violetprouses@gmail.com
Content-Type: multipart/alternative; boundary="000000000000b74b2a0659246f13"

--000000000000b74b2a0659246f13
Content-Type: text/plain; charset="UTF-8"; format=flowed; delsp=yes
Content-Transfer-Encoding: base64

RmFtaWx5IGdyb3VwIHdlbGNvbWUgZW1haWwNCllvdSd2ZSBjcmVhdGVkIGEgZmFtaWx5IGdyb3Vw
DQoNCnZpb2xldHByb3VzZXNAZ21haWwuY29tIDwjPg0KDQpIaSB2aW9sZXQsDQoNCk5vdyB5b3Ug
Y2FuIGNvbm5lY3Qgd2l0aCB5b3VyIGZhbWlseSBvbiBHb29nbGUgYW5kIHNoYXJlIHRoZSBhcHBz
IGFuZCAgDQpzZXJ2aWNlcyB0aGF0IGFyZSByaWdodCBmb3IgeW91Lg0KDQpUbyBnZXQgc3RhcnRl
ZCwgaW52aXRlIG1vcmUgcGVvcGxlIHRvIGpvaW4geW91ciBmYW1pbHkgZ3JvdXAuDQpHZXQgc3Rh
cnRlZCA8aHR0cHM6Ly9teWFjY291bnQuZ29vZ2xlLmNvbS9mYW1pbHkvaW52aXRlbWVtYmVycz4N
CkJyaW5nIHlvdXIgZmFtaWx5IHRvZ2V0aGVyIG9uIEdvb2dsZQ0KU2V0IGRpZ2l0YWwgZ3JvdW5k
IHJ1bGVzIGZvciBraWRzDQoNCkhlbHAgZ3VpZGUgY2hpbGRyZW4gYW5kIHRlZW5zIG9ubGluZSB3
aXRoIEZhbWlseSBMaW5r4oCZcyBwYXJlbnRhbCBjb250cm9sICANCmZlYXR1cmVzDQpLZWVwIGV2
ZXJ5b25lIG9uIHRyYWNrDQoNClN0YXkgb3JnYW5pemVkIGF0IHdvcmsgYW5kIGF0IGhvbWUgd2l0
aCBhIHNoYXJlZCBmYW1pbHkgY2FsZW5kYXINClNoYXJlIGVudGVydGFpbm1lbnQNCg0KU3Vic2Ny
aWJlIHRvIFlvdVR1YmUgUHJlbWl1bSBhbmQgc2hhcmUgYSBtZW1iZXJzaGlwIHdpdGggdGhlIHdo
b2xlIGZhbWlseQ0KQ29ubmVjdCB3aXRoIHlvdXIgZmFtaWx5DQoNCktlZXAgaW4gdG91Y2ggdXNp
bmcgR29vZ2xlIEFzc2lzdGFudOKAmXMgVGVsbCBteSBmYW1pbHksIGxvY2F0aW9uIHNoYXJpbmcs
ICANCmFuZCBwaG90byBzaGFyaW5nIGZlYXR1cmVzDQpHZXQgbW9yZSBzdG9yYWdlDQoNCkdvb2ds
ZSBPbmUgbWVtYmVycyBjYW4gZ2l2ZSBmYW1pbHkgZ3JvdXAgbWVtYmVycyB0aGVpciBvd24gc3Bh
Y2UgdG8gc3RvcmUgIA0KcGVyc29uYWwgZmlsZXMsIGVtYWlscywgYW5kIHBob3Rvcw0KU2hhcmUg
YXBwcyAmIHB1cmNoYXNlcw0KDQpTaGFyZSBodW5kcmVkcyBvZiBnYW1lcyBhbmQgYXBwcyBhcyBh
IGZhbWlseSB3aXRoIFBsYXkgRmFtaWx5IExpYnJhcnkgYXQgbm8gIA0KYWRkaXRpb25hbCBjb3N0
DQpMZWFybiBtb3JlIDxodHRwczovL2cuY28veW91cmZhbWlseT4NCg0KWW91IHJlY2VpdmVkIHRo
aXMgbWFuZGF0b3J5IGVtYWlsIHNlcnZpY2UgYW5ub3VuY2VtZW50IHRvIHVwZGF0ZSB5b3UgYWJv
dXQgIA0KaW1wb3J0YW50IGNoYW5nZXMgdG8geW91ciBHb29nbGUgcHJvZHVjdCBvciBhY2NvdW50
LsKpMjAyNiBHb29nbGUgTExDLCAxNjAwICANCkFtcGhpdGhlYXRyZSBQYXJrd2F5LCBNb3VudGFp
biBWaWV3LCBDQSA5NDA0MywgVVNBDQoNCg0K
--000000000000b74b2a0659246f13
Content-Type: text/html; charset="UTF-8"
Content-Transfer-Encoding: quoted-printable

<head><title>Family group welcome email</title><link rel=3Dstylesheet href=
=3Dhttps://fonts.googleapis.com/css2?family=3DGoogle+Sans:wght@400;500&fami=
ly=3DRoboto:wght@400;500&display=3Dswap nonce=3DcPRb6Cdes0cl2dLDKDUWdQ /><m=
eta http-equiv=3DContent-Type content=3D"text/html; charset=3Dutf-8"></head=
><body style=3D"background: #fff; font: 400 24px Google Sans; margin: auto;=
 max-width: 600px; min-width: 348px; padding: 0 0;"><img src=3D"https://not=
ifications.googleapis.com/email/t/AFG8qyWGtmbq5XyMLiBbUBUyNEuQ79jSsITpjXl6e=
EJuBI_TCpzDdtchJ4Puvz9kZ5TQassixnLvEsMl0QTcbkvfdUn-ppkNkjErNkkm21_YxRZqC19o=
URlLkBfalRVw3X1baECthmNK3_-RXTiHvS3PZsmCHzOexhgfyhw83RF_ZrTkPknSa8Xz2KQv-VL=
MX_MBYS8aqd2OwTzzG5tbXbR-cfACD5wHObvez5XAe9c-0HRRc80cPjX7l8Qz14ZyITWWx2-WRE=
FYijq3M0F6L3CpEUPtQwHmEUmXJKW8ZFD19P_Yux7Z7nJ95L7G0Ybh4km1PHZt8qXhmPqLaLIm6=
pP-0mDuvvINrDheY0BFOXvZA6TrmJaowRcWnpJSPfexRVDxqwmNneOpTEZhuVTtHCpvdvR6dLjM=
oZJrwLkITYEY/a.gif" width=3D1 height=3D1><div style=3D"background: #fff; bo=
x-sizing: border-box; margin: auto; max-width: 500px;border: 1px solid #e8e=
aed; padding: 32px 16px; border-radius: 8px;"><div style=3D"padding:0 0  10=
px ;"><img style=3D"display: block; height: 32px; margin:auto; padding: 0 0=
;" src=3Dhttps://ssl.gstatic.com/images/branding/googlelogo/2x/googlelogo_c=
olor_120x44dp.png alt=3D"" /></div><h1 style=3D"margin: 0; text-align: cent=
er; font: 400 24px 'Google Sans',Roboto,Helvetica,Arial,sans-serif;color: #=
202124; line-height: 32px; padding: 0 0 10px;">You&#39;ve created a family =
group</h1><table role=3DPresentation style=3D"text-align: center;margin: 8p=
x auto 0 auto;"><tr><td style=3D"height: 21px; width: 25px; text-align: cen=
ter; vertical-align: middle;"><img style=3D"display:inline-block; margin:0 =
auto; border-radius:50%; height: 20px; width: 20px;" src=3Dhttps://lh3.goog=
leusercontent.com/a/ACg8ocJrhPBpmUK_IFDl8noxrOXR7QlTa0_gnVg4FxAiIS38TMV9Uw=
=3Ds20-cc alt=3D"" /></td><td><p style=3D"font: 500 14px 'Google Sans',Robo=
to,Helvetica,Arial,sans-serif; line-height: 16px; margin: 0; padding: 1px 1=
px;"><a rel=3Dnofollow href=3D"https://notifications.googleapis.com/email/r=
edirect?t=3DAFG8qyUS3M0FNiqYE1k4XdMQPxX0uKtWEjUpbDOS9U-1H5TVKecSnhEJ3fRhIgL=
omcehmNE8wJILtBX3fhA9Ib4LOHz53-ZiQ7Oa5cs-vCIpBdawq9PUhYQ8-3_LXJ6sX_7j7GhAME=
6LnYf1Hfi6imfJxfixFYG6YqGcNGTPF7vbb8e65VziwrsdzaSl9FMMt3FGGPh4kX2lEFv-a3dro=
l5edGj0Ekoiul4MxEA07_DQ2i3eGcHv3rU709MM0Jlsj-eHWZLL3jnkAbTBnHPe7huPxn1N_WJy=
2XRCwl-9JV_vDGuRSxcW&amp;r=3DeJxTBgAAJAAk&amp;s=3DALHZ2r4tKEDLDIjrpOP4hoQ8-=
dUr" style=3D"text-decoration: none;color: #3c4043;cursor: text">violetprou=
ses@gmail.com</a></p></td></tr></table><div style=3D"border: 1px solid #dad=
ce0; margin: 24px 0"></div><p style=3D"color:#202124; max-width: 456px; let=
ter-spacing: 0.2px; font: 400 14px &#39;Google Sans&#39;,Roboto,Helvetica,A=
rial,sans-serif;line-height: 20px; margin: 24px 0;">Hi violet,</p><p style=
=3D"color:#202124; max-width: 456px; letter-spacing: 0.2px; font: 400 14px =
&#39;Google Sans&#39;,Roboto,Helvetica,Arial,sans-serif;line-height: 20px; =
margin: 24px 0;">Now you can connect with your family on Google and share t=
he apps and services that are right for you.</p><p style=3D"color:#202124; =
max-width: 456px; letter-spacing: 0.2px; font: 400 14px &#39;Google Sans&#3=
9;,Roboto,Helvetica,Arial,sans-serif;line-height: 20px; margin: 24px 0;">To=
 get started, invite more people to join your family group.</p><div style=
=3D"margin: 0 auto; max-width:456px; text-align:center;"><a style=3D"color:=
 #fff; letter-spacing: 0.25px; display: inline-block; text-align: center; t=
ext-decoration:none; font: 500 14px 'Google Sans',Roboto,Helvetica,Arial,sa=
ns-serif;padding: 8px 24px; background: #1a73e8; border-radius: 4px; line-h=
eight: 20px;" href=3D"https://notifications.googleapis.com/email/redirect?t=
=3DAFG8qyVN2-rqXSPDZtI_IuPtX-gGVM1d3BPXFYGhpEZbFB9SuhCrnSwFVBaoF6z-BVnoHW4A=
pT_TAWtihfLoAxVaEyJ-AMjq6DbxjaS_tFGDo4PCLYKoHnpw1fdkf59k3CrkhXDMpgU4z7cMbYE=
Xdqs47xTg33Yxo22nFRqTA2TslFNVGv3pE0xkEWj3KxY9c_1jUM0-mde_aceWaYYZ_ya5NFbdTG=
VHpyu9TM4Pym_7SXiTtri8Y88u-k74B79zBf61Hr4bGnwab5YHxZtv71vcwCbLEo_Ea9SEWOWGN=
6dA8pDM-eKIl9v7SDSRcbg4JEdqbbcpmBnGd17uhOSu0jHhqA&amp;r=3DeJwFwdENABAMBcCN9=
N82NEUTT4WS2N5dc587EuElZjvDQzWrXQIbqCRof6TjqgsEWdb-1MITEQ&amp;s=3DALHZ2r71G=
2u0FWRjsHeVxgetuk0t">Get started</a></div><div style=3D"border: 1px solid #=
dadce0; margin: 24px 0"></div><h2 style=3D"color: #202124; font: 700 15px '=
Google Sans',Roboto,Helvetica,Arial,sans-serif; line-height: 20px; text-ali=
gn: center; ">Bring your family together on Google</h2><table class=3Dvalue=
PropositionItem role=3DPresentation style=3D"margin: 24px auto 0;border-spa=
cing: 32px 0"><tr><td><table style=3D"border-spacing: 0; background: no-rep=
eat center url(https://www.gstatic.com/family/emails/value_prop_set_digital=
_ground_rules_for_kids_51b6597434450da2087040b0017fd8d7.png); background-si=
ze: 128px; width: 128px; height: 128px;"><tr><td></td><td style=3D"width: 4=
5px; height: 83px;"></td></tr><tr><td style=3D"width: 83px; height: 45px;">=
</td><td style=3D"width: 45px; height: 45px; text-align: center; vertical-a=
lign: middle; background: no-repeat center url(https://www.gstatic.com/fami=
ly/emails/value_prop_mini_image_holder.png);"><img style=3D"display:block; =
margin:0 auto;" width=3D26px height=3D26px src=3Dhttps://ssl.gstatic.com/fa=
mily/familylink/family_link_40.png alt=3D""></td></tr></table></td><td styl=
e=3D"width: 277px;"><table role=3DPresentation><tr><td><h3 style=3D"color: =
#3c4043; font: 700 14px 'Google Sans',Roboto,Helvetica,Arial,sans-serif; li=
ne-height: 20px; margin: 0; ">Set digital ground rules for kids</h3></td></=
tr><tr><td><p style=3D"color: #3c4043; font: 400 14px 'Google Sans',Roboto,=
Helvetica,Arial,sans-serif; line-height: 20px; margin: 0;">Help guide child=
ren and teens online with Family Link=E2=80=99s parental control features</=
p></td></tr></table></td></tr></table><table class=3DvaluePropositionItem r=
ole=3DPresentation style=3D"margin: 24px auto 0;border-spacing: 32px 0"><tr=
><td style=3D"width: 277px;"><table role=3DPresentation><tr><td><h3 style=
=3D"color: #3c4043; font: 700 14px 'Google Sans',Roboto,Helvetica,Arial,san=
s-serif; line-height: 20px; margin: 0; ">Keep everyone on track</h3></td></=
tr><tr><td><p style=3D"color: #3c4043; font: 400 14px 'Google Sans',Roboto,=
Helvetica,Arial,sans-serif; line-height: 20px; margin: 0;">Stay organized a=
t work and at home with a shared family calendar</p></td></tr></table></td>=
<td><table style=3D"border-spacing: 0; background: no-repeat center url(htt=
ps://www.gstatic.com/family/emails/value_prop_keep_everyone_on_track_790ea7=
29e48f339ac8c42a6de4ff3bda.png); background-size: 128px; width: 128px; heig=
ht: 128px;"><tr><td></td><td style=3D"width: 45px; height: 83px;"></td></tr=
><tr><td style=3D"width: 45px; height: 45px; text-align: center; vertical-a=
lign: middle; background: no-repeat center url(https://www.gstatic.com/fami=
ly/emails/value_prop_mini_image_holder.png);"><img style=3D"display:block; =
margin:0 auto;" width=3D26px height=3D26px src=3Dhttps://ssl.gstatic.com/ca=
lendar/images/dynamiclogo_2020q4/calendar_20_2x.png alt=3D""></td><td style=
=3D"width: 83px; height: 45px;"></td></tr></table></td></tr></table><table =
class=3DvaluePropositionItem role=3DPresentation style=3D"margin: 24px auto=
 0;border-spacing: 32px 0"><tr><td><table style=3D"border-spacing: 0; backg=
round: no-repeat center url(https://www.gstatic.com/family/emails/value_pro=
p_share_entertainment_8c30b30dc635bc70857bccc73f1a9125.png); background-siz=
e: 128px; width: 128px; height: 128px;"><tr><td></td><td style=3D"width: 45=
px; height: 83px;"></td></tr><tr><td style=3D"width: 83px; height: 45px;"><=
/td><td style=3D"width: 45px; height: 45px; text-align: center; vertical-al=
ign: middle; background: no-repeat center url(https://www.gstatic.com/famil=
y/emails/value_prop_mini_image_holder.png);"><img style=3D"display:block; m=
argin:0 auto;" width=3D26px height=3D26px src=3Dhttps://ssl.gstatic.com/fam=
ily/webhome/yt-icon_128x128_e65cc1f2a3b7bf766fc1009d4558d6ee.png alt=3D""><=
/td></tr></table></td><td style=3D"width: 277px;"><table role=3DPresentatio=
n><tr><td><h3 style=3D"color: #3c4043; font: 700 14px 'Google Sans',Roboto,=
Helvetica,Arial,sans-serif; line-height: 20px; margin: 0; ">Share entertain=
ment</h3></td></tr><tr><td><p style=3D"color: #3c4043; font: 400 14px 'Goog=
le Sans',Roboto,Helvetica,Arial,sans-serif; line-height: 20px; margin: 0;">=
Subscribe to YouTube Premium and share a membership with the whole family</=
p></td></tr></table></td></tr></table><table class=3DvaluePropositionItem r=
ole=3DPresentation style=3D"margin: 24px auto 0;border-spacing: 32px 0"><tr=
><td style=3D"width: 277px;"><table role=3DPresentation><tr><td><h3 style=
=3D"color: #3c4043; font: 700 14px 'Google Sans',Roboto,Helvetica,Arial,san=
s-serif; line-height: 20px; margin: 0; ">Connect with your family</h3></td>=
</tr><tr><td><p style=3D"color: #3c4043; font: 400 14px 'Google Sans',Robot=
o,Helvetica,Arial,sans-serif; line-height: 20px; margin: 0;">Keep in touch =
using Google Assistant=E2=80=99s Tell my family, location sharing, and phot=
o sharing features</p></td></tr></table></td><td><table style=3D"border-spa=
cing: 0; background: no-repeat center url(https://www.gstatic.com/family/em=
ails/value_prop_connect_with_your_family_5114b153c3b2ed0e3a9c36391b66ee99.p=
ng); background-size: 128px; width: 128px; height: 128px;"><tr><td></td><td=
 style=3D"width: 45px; height: 83px;"></td></tr><tr><td style=3D"width: 45p=
x; height: 45px; text-align: center; vertical-align: middle; background: no=
-repeat center url(https://www.gstatic.com/family/emails/value_prop_mini_im=
age_holder.png);"><img style=3D"display:block; margin:0 auto;" width=3D26px=
 height=3D26px src=3Dhttps://ssl.gstatic.com/family/webhome/ic_assistant.pn=
g alt=3D""></td><td style=3D"width: 83px; height: 45px;"></td></tr></table>=
</td></tr></table><table class=3DvaluePropositionItem role=3DPresentation s=
tyle=3D"margin: 24px auto 0;border-spacing: 32px 0"><tr><td><table style=3D=
"border-spacing: 0; background: no-repeat center url(https://www.gstatic.co=
m/family/emails/value_prop_get_more_storage_43535ac015b32594abd17e45b478f32=
f.png); background-size: 128px; width: 128px; height: 128px;"><tr><td></td>=
<td style=3D"width: 45px; height: 83px;"></td></tr><tr><td style=3D"width: =
83px; height: 45px;"></td><td style=3D"width: 45px; height: 45px; text-alig=
n: center; vertical-align: middle; background: no-repeat center url(https:/=
/www.gstatic.com/family/emails/value_prop_mini_image_holder.png);"><img sty=
le=3D"display:block; margin:0 auto;" width=3D26px height=3D26px src=3Dhttps=
://ssl.gstatic.com/subscriptions/img/logo_one_64px.png alt=3D""></td></tr><=
/table></td><td style=3D"width: 277px;"><table role=3DPresentation><tr><td>=
<h3 style=3D"color: #3c4043; font: 700 14px 'Google Sans',Roboto,Helvetica,=
Arial,sans-serif; line-height: 20px; margin: 0; ">Get more storage</h3></td=
></tr><tr><td><p style=3D"color: #3c4043; font: 400 14px 'Google Sans',Robo=
to,Helvetica,Arial,sans-serif; line-height: 20px; margin: 0;">Google One me=
mbers can give family group members their own space to store personal files=
, emails, and photos</p></td></tr></table></td></tr></table><table class=3D=
valuePropositionItem role=3DPresentation style=3D"margin: 24px auto 0;borde=
r-spacing: 32px 0"><tr><td style=3D"width: 277px;"><table role=3DPresentati=
on><tr><td><h3 style=3D"color: #3c4043; font: 700 14px 'Google Sans',Roboto=
,Helvetica,Arial,sans-serif; line-height: 20px; margin: 0; ">Share apps &am=
p; purchases</h3></td></tr><tr><td><p style=3D"color: #3c4043; font: 400 14=
px 'Google Sans',Roboto,Helvetica,Arial,sans-serif; line-height: 20px; marg=
in: 0;">Share hundreds of games and apps as a family with Play Family Libra=
ry at no additional cost</p></td></tr></table></td><td><table style=3D"bord=
er-spacing: 0; background: no-repeat center url(https://www.gstatic.com/fam=
ily/emails/value_props_share_apps_and_purchases_328eaeb79dd2cdfd2439b99f9fd=
21e89.png); background-size: 128px; width: 128px; height: 128px;"><tr><td><=
/td><td style=3D"width: 45px; height: 83px;"></td></tr><tr><td style=3D"wid=
th: 45px; height: 45px; text-align: center; vertical-align: middle; backgro=
und: no-repeat center url(https://www.gstatic.com/family/emails/value_prop_=
mini_image_holder.png);"><img style=3D"display:block; margin:0 auto;" width=
=3D26px height=3D26px src=3Dhttps://ssl.gstatic.com/family/webhome/ic_playf=
amilylibrary_cd597b28d31fa4286d1375752de3563f.png alt=3D""></td><td style=
=3D"width: 83px; height: 45px;"></td></tr></table></td></tr></table><div st=
yle=3D"margin: 24px auto 8px; max-width:456px; text-align:center;"><a style=
=3D"border: 2px solid #e8eaed; border-radius: 4px; color: #1a73e8; display:=
 inline-block; font: 500 14px 'Google Sans',Roboto,Helvetica,Arial,sans-ser=
if; letter-spacing: 0.25px; line-height: 20px; padding: 8px 20px; text-deco=
ration:none;" href=3D"https://notifications.googleapis.com/email/redirect?t=
=3DAFG8qyUpFQLU2OcJxtfZRfYC4WqU9ehVwaJ1DeO4YCj3d-YrzGs4Hwyk3mlBvRyu1Z9qr4G1=
T8cU0SN1cbXI0l9UkZcK47FrGCPxOjmLdqTRqTPsSSWma494jIQ8jhKA3PA_nAMk6buobesT4ls=
KlJjS5Tqv4yJ9aAeQRFiVp1sZwqFuC6kgGt3aGOhnrx9WJmz8cDuzgs1GVCymx9Ek1QbuB9nCUj=
sNor4Sse0ZCKv06HVCir5UaNXKZVaERvibBbvCNtH0gBe08tIvINCb1PyeVwfZxfFGXbIqIgCwR=
XGfj1y0s55Y7Pmd6M7gtp3uUki1Go-BLHN5YA&amp;r=3DeJzLKCkpKLbS10_XS87Xr8wvLUpLz=
M3MqQQAZRQIsw&amp;s=3DALHZ2r4Kg248SreLTqt5fl50jpBI">Learn more</a></div></d=
iv><footer style=3D"max-width: 499px; color: #888; margin: auto; font: 400 =
11px 'Google Sans',Roboto,Helvetica,Arial,sans-serif;letter-spacing: 0.2px;=
"><p>You received this mandatory email service announcement to update you a=
bout important changes to your Google product or account.<span>&copy;2026 G=
oogle LLC, 1600 Amphitheatre Parkway, Mountain View, CA 94043, USA</span></=
p></footer></body>
--000000000000b74b2a0659246f13--

From 1873661146655332909@xxx Sun Aug 16 06:41:53 +0000 2026
X-GM-THRID: 1873661146655332909
X-Gmail-Labels: Inbox,Opened,Category Updates
Delivered-To: violetprouses@gmail.com
Received: by 2002:a17:504:b30a:20b0:1e7e:8814:2405 with SMTP id e10-n2csp1481842njt;
        Sat, 15 Aug 2026 23:41:53 -0700 (PDT)
X-Received: by 2002:a05:690c:6081:b0:81f:c2dc:6870 with SMTP id 00721157ae682-8370ea71c78mr68044387b3.15.1786862513578;
        Sat, 15 Aug 2026 23:41:53 -0700 (PDT)
ARC-Seal: i=1; a=rsa-sha256; t=1786862513; cv=none;
        d=google.com; s=arc-20260327;
        b=Y+NhKxN03ty+OnEv16VNpCYWp+bNk5u0EvnCLRhTBJj9N9aA/ubdsPMvoud5CF2d9a
         k0zNeTZ4H2aRNwRk+ZJfMAc4maARKOzbPNDBTRA3q31VJksYxy+CsuJP4x5lSGp4Wv/u
         NFglF//hLeDsuerh/+R9WZwpMwZuzT55NQMr/+/74hQsb2wUyFRN4ygmX3AccTTRBOU+
         eWiUG7UF1Pzj0lSXWi4aGopnrXg+oLa+j7oUPhKfa90BUaYj0HvuigB18W2WmwcJ8fkQ
         R/PkSjWlwdFGZSOntEVbA9n6u60gKiHvdgg5X7CpG5U8kaU3+u4VtfRuu43ysDb+ALak
         HDig==
ARC-Message-Signature: i=1; a=rsa-sha256; c=relaxed/relaxed; d=google.com; s=arc-20260327;
        h=to:from:subject:message-id:gmsai:list-unsubscribe
         :list-unsubscribe-post:feedback-id:list-id:date:mime-version
         :dkim-signature;
        bh=1In+zAxaxgf+h6/Z5tfIPN9Wq45ZR7XXbPfb1zSCXqk=;
        fh=hUfB+x8fKgVbMvTJ7mEk0I28xQ+Z9a/Un/iVPLaMuVQ=;
        b=kcSEbwFm5+wU7cLjkYRG3hhJNryly0wuIUBIuIe80//E3M55vo+302C20lXW7yIR5t
         VkYQNoj9F9VTGd/nbtYf2VkN3ttrl1Rjo3VVBoN/gLNCoonmuSLpuBvp+S3u/CXjO90K
         8PMJIj6HTFCr8b733XdfnIke4L9JMXWwqrdSBXOuxUkECK3qtmPMp7lWMtxY3Yo4hGT2
         SIf0pTj9KgAEEq0IlhzZMDalKT1MZMFP9MPs4umZE9YvUG4HoH3nVqYlpkCfbFuZDAd5
         nAw287vSzcxL16uYKxRi16+Q5Vu1N7In06r1RLfmf83MjV9XU29wKL2HlfBh1UPbzo7I
         LbKg==;
        dara=google.com
ARC-Authentication-Results: i=1; mx.google.com;
       dkim=pass header.i=@google.com header.s=20251104 header.b=mz6lfhqe;
       spf=pass (google.com: domain of 3rfubahakdcmwx0nyu7-jllx3w21pxxpun.lxv4rxun2y0x31n1pvjru.lxv@scoutcamp.bounces.google.com designates 209.85.220.69 as permitted sender) smtp.mailfrom=3rFuBahAKDcMwx0nyu7-jllx3w21pxxpun.lxv4rxun2y0x31n1pvjru.lxv@scoutcamp.bounces.google.com;
       dmarc=pass (p=REJECT sp=REJECT dis=NONE) header.from=google.com;
       dara=pass header.i=@gmail.com
Return-Path: <3rFuBahAKDcMwx0nyu7-jllx3w21pxxpun.lxv4rxun2y0x31n1pvjru.lxv@scoutcamp.bounces.google.com>
Received: from mail-sor-f69.google.com (mail-sor-f69.google.com. [209.85.220.69])
        by mx.google.com with SMTPS id 00721157ae682-836bbbc5407sor81327287b3.5.2026.08.15.23.41.48
        for <violetprouses@gmail.com>
        (Google Transport Security);
        Sat, 15 Aug 2026 23:41:53 -0700 (PDT)
Received-SPF: pass (google.com: domain of 3rfubahakdcmwx0nyu7-jllx3w21pxxpun.lxv4rxun2y0x31n1pvjru.lxv@scoutcamp.bounces.google.com designates 209.85.220.69 as permitted sender) client-ip=209.85.220.69;
Authentication-Results: mx.google.com;
       dkim=pass header.i=@google.com header.s=20251104 header.b=mz6lfhqe;
       spf=pass (google.com: domain of 3rfubahakdcmwx0nyu7-jllx3w21pxxpun.lxv4rxun2y0x31n1pvjru.lxv@scoutcamp.bounces.google.com designates 209.85.220.69 as permitted sender) smtp.mailfrom=3rFuBahAKDcMwx0nyu7-jllx3w21pxxpun.lxv4rxun2y0x31n1pvjru.lxv@scoutcamp.bounces.google.com;
       dmarc=pass (p=REJECT sp=REJECT dis=NONE) header.from=google.com;
       dara=pass header.i=@gmail.com
DKIM-Signature: v=1; a=rsa-sha256; c=relaxed/relaxed;
        d=google.com; s=20251104; t=1786862508; x=1787467308; dara=google.com;
        h=content-type:to:from:subject:message-id:gmsai:list-unsubscribe
         :list-unsubscribe-post:feedback-id:list-id:date:mime-version:from:to
         :cc:subject:date:message-id:reply-to:content-type;
        bh=1In+zAxaxgf+h6/Z5tfIPN9Wq45ZR7XXbPfb1zSCXqk=;
        b=mz6lfhqeiSBJECA/4JCoPRnNWAGdLb2Zuj+qYd6Fw4lewZhAPpFIJNh3HgFs3HNtpd
         ziOxuiXpOJ3rC/IxtLyBTQOkyPvtBNYFTR8aZO94JmJ6oQhVAePcgSa2Qs36iPV+9tnD
         7r+siW5g8//2zca/mIzugVify8wW0i4pAZw7FnAXjqqzJujaVVqvSBR10hUPSOLEOD9X
         EiY3fFbRFT/3jSkvBvdBRfrAQnxbLmumoKDjImuQa8/wbIXqC2wzOF7EXq9rjYhSZVEZ
         kj9kqsSD1MmABupoC1uaHzveS2MLycI6ZSB6VTyxBV+wjCzLZ0wXoGgOaWX0WG6bkNpG
         Jb+A==
X-Google-DKIM-Signature: v=1; a=rsa-sha256; c=relaxed/relaxed;
        d=1e100.net; s=20251104; t=1786862508; x=1787467308;
        h=content-type:to:from:subject:message-id:gmsai:list-unsubscribe
         :list-unsubscribe-post:feedback-id:list-id:date:mime-version
         :x-gm-message-state:from:to:cc:subject:date:message-id:reply-to
         :content-type;
        bh=1In+zAxaxgf+h6/Z5tfIPN9Wq45ZR7XXbPfb1zSCXqk=;
        b=aGO2VS7HHvbz54DmKS85fe2clbLFHAoekwGVtMjKgf4OumE0jI/5+8+ASR0yhJbLs9
         Et6Xzwvpp9JsTo8K681A67SEUDEa3XNT4S0rQIbI7FqT4g01XsPAt5+aPR5oysDc9hla
         4OBKArQN6W2Saj0JXY+hRE79UmrR7Uyr54x+4c/HrjTREujXDAcU1sWEfGHwpzsEMXvi
         JPJ244altFOcie9KEsoTTWaGL6NinpfDeyuKpic+Oxx+CAh13WZLJUrPo34tEGZTLEVq
         1Q3Cme9jnkPuG+ZCMnl9xu4ZKbgalTHcmhlOJAlh5TcBVP978Eet8XrPw4Do8iJjirZq
         2www==
X-Gm-Message-State: AOJu0YxhPdeIk+Vv3zb2lJBMrgcRDcAFjXb1AIOgNXTMrQrhoP/ex9qY
	MCD9s7OAQ+4WqUVH4NvZWmAsbuE80uJKy/SEpkR0atU42e4YZArEszo0uBGW
MIME-Version: 1.0
X-Received: by 2002:a05:690e:b8c:b0:66b:15f3:97f5 with SMTP id
 956f58d0204a3-66c72b06b12mr5961394d50.9.1786862508543; Sat, 15 Aug 2026
 23:41:48 -0700 (PDT)
Date: Sat, 15 Aug 2026 23:41:48 -0700
List-Id: <98b5bb09ff6ac9c617e21f7ba54977101832eb6f2a63fd56caa2f008f240e7f6@google.com>
Feedback-ID: Pb03ba12bf7-8399789e22:C9149520350:M111271686-en:gamma
List-Unsubscribe-Post: List-Unsubscribe=One-Click
List-Unsubscribe: <https://myaccount.google.com/communication-preferences/auto/unsubscribe/gt/AKMee0cW2nAB43XYf6HWrwG9GAUL5tEAgmZAM-HVy-WDpg33r6HZaoX9QJvIMhYkabviGgbxnCUyCSDOQxIz3qYJxJKvosGIJ4Tvj9opR2cMHZaap2_y4AtBZJc0QKLEFDcjscBI7BpOEVBp1ikfyjDPVgUdfHPuRZdeam_oL7SUo-93SZ6XExqZzSCm2OnMjpE8tjS4BQYYTazxq8e_-AzOLFhQbqwEVlGZHGWgSn9jjet7j1Xgy63uS2e_oJcrohpHtuC1yGtV_FFtS2if3DybeZmQgn1ErBkqVo0ZMO9kRyTT?utm_source=gm_header&utm_medium=email>
gmsai: false
X-Google-Notification-Metadata: EgA
X-Notifications: 677527871355-1094401754600-CONNECTION_SOURCE_OAUTH-1786862496
X-Notifications-Bounce-Info: AWKoMQRjzkGPISG7MqOWPUHRYEQE8Xy3H-gh93cxEJEqXmnhGOfrbiLHXBdQOT3Qhp0GvxSHTUTm7hSfm0zTW6qMXvHr88AxsJfBwjpywLURZvw01J67H01z_EcuI9gE_V7tjPN9WgVDVwv_1vR72gqLcJkHWbbgkBo94wLwNMkaWR3GpV1kDa8mF8beJNrBFNiO4kzk7oUjiqX7JtF6G0XtFYRJkANAisLPgUHNLTmkUqaKmTdd-taOS737HtSonFrRVrIafv3TaOKi2ARH4GHy25Hl-V8Tl-f7IIv2-xPgfKbAN1eqNgJZQ0SS35es7oQlqUeuP2oXdEZf-_1NhgxIGOSdOSaoDiyhpoePTW2oBUgPMAyGbVl5jSLcXQ7BfjvRNphqBp9khqKsQaqqHOxNo1zspj-vIwUjUZt4wdMuM9UBjBJHFFuYMQ33EVFki3wP-HY-xYPlSAJ54jkI1wLJqoad1HcSbn6Cpxu1IjOcMzEhSM_Kbc7xfluRJE9RDibfTWZcKEEgjR2pW_84JnOYgsOvz2Ee2rnP42-8kImIky5Y4QKc4naNbmPIJ24nxjiD0c_8AOtAcEJslJzMuyvR0jSzjSH4y-u2KGYTTDbiG6Rd2ti4niK-q7j6M3d_IzjyGcvQwG-UPxspR1YgHBUqsNANPJpNCAVbXgRyGzMi6N3At0dqWQDVjaLEuO3L6LfVhGuHKlnit16NEXx4ZJsg4A23kKGXX9BsHh-ktjAqQcGPEyQ-a9_0gAqrQ2nHLCq9e6a5i93IciCZ3dPJjX-e7m6chMbPIa0qjx63PIlbQYdhJjMvZME2eTOnGRd3FVvprbmX-SZuabCvKJBOT4p4MWv_H1syeiNP_Eb_IFwUvy8k1M8ra1As2tfe-wNjAwNjA0MDQxNTM1NTk2OTMzMg
Message-ID: <8106742c92fb74c63d3b4ea3e70454ae68aa9d04-20376977-337030291@google.com>
Subject: You shared some Google Account data with ecosia.org
From: Google <noreply-accounts@google.com>
To: violetprouses@gmail.com
Content-Type: multipart/alternative; boundary="00000000000015913906592459b2"

--00000000000015913906592459b2
Content-Type: text/plain; charset="UTF-8"; format=flowed; delsp=yes
Content-Transfer-Encoding: base64

S2VlcCB0cmFjayBvZiB5b3VyIEdvb2dsZSBBY2NvdW50IGRhdGENCg0KDQoNCnZpb2xldHByb3Vz
ZXNAZ21haWwuY29tDQoNCuKAig0KDQo8IS0tW2lmICFtc29dPjwhLS0+DQoNCjwhLS1baWYgZmFs
c2VdPjwhLS0+DQoNCg0KWW91J3JlIHJlY2VpdmluZyB0aGlzIGVtYWlsIGJlY2F1c2UgeW91IHVz
ZWQgU2lnbiBpbiB3aXRoIEdvb2dsZSB0byBzaWduIGluICANCnRvDQoNCg0KPGh0dHBzOi8vYy5n
bGUvQUtNZWUwZDROODhQQnZ0ZER6RGRnTEMtemNnckcwMjN4djVMdVR2ZXEyUW9BbC1sRnRVeXFp
VGs5ODdiZDVLdXdLOUpjRUZuUGFzTUlwaFNoT01ZNVlRZ2JSaFV2NU91T0F3bmlQZzNGanVqNkxq
ZllxST5lY29zaWEub3JnDQoNCg0Kb24gQXVndXN0IDE2IGF0IDY6NDHigK9BTSBHTVQrMCAuDQoN
ClRoaXMgZW1haWwgc3VtbWFyaXplcyB0aGUgaW5mbyB5b3Ugc2hhcmVkLiBUaGVyZeKAmXMgbm90
aGluZyB5b3UgbmVlZCB0byBkbyAgDQpyaWdodCBub3cuDQoNCg0KPCEtLVtpZiAhbXNvXT48IS0t
Pg0KDQo8IS0tW2lmIGZhbHNlXT48IS0tPg0KDQo8IS0tW2lmIGZhbHNlXT48IS0tPg0KDQpZb3Un
cmUgcmVjZWl2aW5nIHRoaXMgZW1haWwgYmVjYXVzZSB5b3UgdXNlZCBTaWduIGluIHdpdGggR29v
Z2xlIHRvIHNpZ24gaW4gIA0KdG8NCg0KDQo8aHR0cHM6Ly9jLmdsZS9BS01lZTBkNE44OFBCdnRk
RHpEZGdMQy16Y2dyRzAyM3h2NUx1VHZlcTJRb0FsLWxGdFV5cWlUazk4N2JkNUt1d0s5SmNFRm5Q
YXNNSXBoU2hPTVk1WVFnYlJoVXY1T3VPQXduaVBnM0ZqdWo2TGpmWXFJPmVjb3NpYS5vcmcNCg0K
DQpvbiBBdWd1c3QgMTYgYXQgNjo0MeKAr0FNIEdNVCswIC4NCg0KVGhpcyBlbWFpbCBzdW1tYXJp
emVzIHRoZSBpbmZvIHlvdSBzaGFyZWQuIFRoZXJl4oCZcyBub3RoaW5nIHlvdSBuZWVkIHRvIGRv
ICANCnJpZ2h0IG5vdy4NCg0KPCEtLVtpZiBmYWxzZV0+PCEtLT4NCg0KDQplY29zaWEub3JnIHJl
Y2VpdmVkIHRoaXMgcHJvZmlsZSBpbmZvDQoNCg0KDQp2aW9sZXQgc21pdGgNCg0KTmFtZSBhbmQg
cHJvZmlsZSBwaWN0dXJlDQoNCg0KDQp2aW9sZXRwcm91c2VzQGdtYWlsLmNvbQ0KDQpFbWFpbCBh
ZGRyZXNzDQoNCg0KDQoNCg0K4oCKDQoNCg0KVGhpcyBlbWFpbCBpbmNsdWRlcyB0aGUgaW5mbyB5
b3Ugc2hhcmVkIG9uDQoNCkF1Z3VzdCAxNiBhdCA2OjQx4oCvQU0gR01UKzANCg0KSWYgeW91IHdh
bnQgdG8gc3RvcCB1c2luZyBTaWduIGluIHdpdGggR29vZ2xlIHdpdGgNCg0KZWNvc2lhLm9yZyAs
IGdvIHRvIHlvdXIgR29vZ2xlIEFjY291bnQuDQoNCg0KPCEtLVtpZiAhbXNvXT48IS0tPg0KDQo8
IS0tW2lmIGZhbHNlXT48IS0tPg0KDQo8IS0tW2lmIGZhbHNlXT48IS0tPg0KDQplY29zaWEub3Jn
IHJlY2VpdmVkIHRoaXMgcHJvZmlsZSBpbmZvDQoNCjwhLS1baWYgZmFsc2VdPjwhLS0+DQoNCjwh
LS1baWYgZmFsc2VdPjwhLS0+DQoNCjwhLS1baWYgZmFsc2VdPjwhLS0+DQoNCnZpb2xldCBzbWl0
aA0KDQpOYW1lIGFuZCBwcm9maWxlIHBpY3R1cmUNCg0KPCEtLVtpZiBmYWxzZV0+PCEtLT4NCg0K
PCEtLVtpZiBmYWxzZV0+PCEtLT4NCg0KPCEtLVtpZiBmYWxzZV0+PCEtLT4NCg0KdmlvbGV0cHJv
dXNlc0BnbWFpbC5jb20NCg0KRW1haWwgYWRkcmVzcw0KDQo8IS0tW2lmIGZhbHNlXT48IS0tPg0K
DQo8IS0tW2lmIGZhbHNlXT48IS0tPg0KDQo8IS0tW2lmIGZhbHNlXT48IS0tPg0KDQo8IS0tW2lm
IGZhbHNlXT48IS0tPg0KDQo8IS0tW2lmIGZhbHNlXT48IS0tPg0KDQrigIoNCg0KPCEtLVtpZiBm
YWxzZV0+PCEtLT4NCg0KPCEtLVtpZiBmYWxzZV0+PCEtLT4NCg0KVGhpcyBlbWFpbCBpbmNsdWRl
cyB0aGUgaW5mbyB5b3Ugc2hhcmVkIG9uDQoNCkF1Z3VzdCAxNiBhdCA2OjQx4oCvQU0gR01UKzAN
Cg0KPCEtLVtpZiBmYWxzZV0+PCEtLT4NCg0KSWYgeW91IHdhbnQgdG8gc3RvcCB1c2luZyBTaWdu
IGluIHdpdGggR29vZ2xlIHdpdGgNCg0KZWNvc2lhLm9yZyAsIGdvIHRvIHlvdXIgR29vZ2xlIEFj
Y291bnQuDQoNCjwhLS1baWYgZmFsc2VdPjwhLS0+DQoNCg0KPCEtLVtpZiBtc29dPg0KPHY6cm91
bmRyZWN0IHhtbG5zOnY9InVybjpzY2hlbWFzLW1pY3Jvc29mdC1jb206dm1sIiAgDQp4bWxuczp3
PSJ1cm46c2NoZW1hcy1taWNyb3NvZnQtY29tOm9mZmljZTp3b3JkIiAgDQpocmVmPSJodHRwczov
L2FjY291bnRzLmdvb2dsZS5jb20vQWNjb3VudENob29zZXI/RW1haWw9dmlvbGV0cHJvdXNlc0Bn
bWFpbC5jb20mY29udGludWU9aHR0cHM6Ly9teWFjY291bnQuZ29vZ2xlLmNvbS9jb25uZWN0aW9u
cy9vdmVydmlldy9BV1c1bldRNlNCQ3dOaVlxd2JzMHdTTTlTMWFmVUZpTk10aGsyVFV2VFhBOEFm
N2xreGp2ZHhzRXpCQVEwdExRRXlOQVB0ekE5dDh3czhJM2lEdUZza0FZZS1aZT91dG1fc291cmNl
PWVfbm90aWZpY2F0aW9uJnV0bV9tZWRpdW09ZW1haWxfbm90aWZpY2F0aW9uIiAgDQpzdHlsZT0i
aGVpZ2h0OjQ4cHg7d2lkdGg6MjY4cHg7di10ZXh0LWFuY2hvcjptaWRkbGU7IiBhcmNzaXplPSIx
MjUlIiAgDQpzdHJva2U9ImZhbHNlIiBmaWxsY29sb3I9IiMwYjU3ZDAiPg0KPHc6YW5jaG9ybG9j
ay8+DQo8djp0ZXh0Ym94IGluc2V0PSIwcHgsMHB4LDBweCwwcHgiPg0KDQo8IVtlbmRpZl0tLT4N
CjxodHRwczovL2MuZ2xlL0FLTWVlMGVCVnJOMTBLNjJUb2d1UW0zS00wTDZTTjdNeFdMWVo1RWVN
QkxfQWl3X0pGR3hDTWlRd25qeTFMQ1ZkOTV6blItVDZOR0ROZ3lVVzZUTjV2MHNfaWZROHFZek84
WlBQajVwN09Zbmlka2Z6TUtwUFdFblhNbDdiemdSVno3d0ZHOGJKOTlvUmJ2elpLX2xqNjVxWHh5
T0ZhaHMyb2ZMUE5Yb1FBeXFKTEVvS2pDY0Jhcy1MSEJvcld0T0cyM0wybEpvZlc3UkhCN2hVWlVr
c3lqVWlGWEZPTVR2aThibTI4TWdhb194YkhrNU9YZDhGaU1yVFFpSlZVa2dSbDd0OFpMeUlXS1BJ
c1JvRXVIX19WekVFeU1wUk92SWlXYXI0Ui1KM3dWNEN2Mjdzd3hWUm5waFlYY3E1NmZSSzR4eGRH
ZXpCY3p0Tmp3VnNiOXhJNUM5VWZueFljMkwyS2dqbnlndjhGNUNSb3pxQUJobUtsR3V6WFNEcHZS
VENmQk9XdGVUeENDVDY5dnYxUmI4dlpBODREa3lqR2tlYlVqQW5OanZKa0k0VTZzQXZ5eWVueHAy
MWd5LThremo0T3FzSUFCcUxxZnM+ICANCkdvICANCnRvIHlvdXIgR29vZ2xlIEFjY291bnQNCg0K
DQpSZXZpZXcNCg0KZWNvc2lhLm9yZyDigJlzDQoNClByaXZhY3kgUG9saWN5IGFuZCBUZXJtcyBv
ZiBTZXJ2aWNlIHRvIHVuZGVyc3RhbmQgaG93DQoNCmVjb3NpYS5vcmcNCg0Kd2lsbCBwcm9jZXNz
IGFuZCBwcm90ZWN0IHlvdXIgZGF0YS4NCg0KSWYgeW91IHdhbnQgdG8gZGVsZXRlIHRoZSBkYXRh
IHlvdSBzaGFyZWQgd2l0aA0KDQplY29zaWEub3JnICwNCg0KdmlzaXQNCg0KZWNvc2lhLm9yZyAu
DQoNClNhZmVyIHdpdGggR29vZ2xlDQoNCllvdXIgR29vZ2xlIEFjY291bnQgcHJvdGVjdHMgeW91
ciBwcml2YWN5IHdpdGggYWR2YW5jZWQgc2VjdXJpdHkgZGVzaWduZWQgIA0KdG8ga2VlcCB5b3Vy
IGRhdGEgc2FmZQ0KDQo8IS0tW2lmICFtc29dPjwhLS0+DQoNCjwhLS1baWYgZmFsc2VdPjwhLS0+
DQoNClNhZmVyIHdpdGggR29vZ2xlDQoNCllvdXIgR29vZ2xlIEFjY291bnQgcHJvdGVjdHMgeW91
ciBwcml2YWN5IHdpdGggYWR2YW5jZWQgc2VjdXJpdHkgZGVzaWduZWQgIA0KdG8ga2VlcCB5b3Vy
IGRhdGEgc2FmZQ0KDQoNCuKAig0KDQpZb3UgcmVjZWl2ZWQgdGhpcyBlbWFpbCB0byBsZXQgeW91
IGtub3cgYWJvdXQgaW1wb3J0YW50IGNoYW5nZXMgdG8geW91ciAgDQpHb29nbGUgQWNjb3VudCBh
bmQgc2VydmljZXMuDQoNCklmIHlvdSB3YW50IHRvIHN0b3AgcmVjZWl2aW5nIHRoZXNlIGVtYWls
cywgeW91IGNhbiAgDQo8aHR0cHM6Ly9teWFjY291bnQuZ29vZ2xlLmNvbS9jb21tdW5pY2F0aW9u
LXByZWZlcmVuY2VzL3Vuc3Vic2NyaWJlL2d0L0FLTWVlMGRyMkhCakQ2LUZOdm4xdUZqbkx2LWdX
cUlocnlJVWlQM2Q1ejAybHVibC02dFJQR1VlMGU1S1hrZ1pNbFBRb242cnNwSW9uVjV2R2dzVmZh
bkI0T1RVQ25ta3AyY25UR00xQ2NYcmcxb0plOVVSRW5XaEhlVk1vZEJLSEEwOTBDSUxyU3k5MHU4
MVFITHFIYnB3QWgyamFWRnBDaWJ0TzdLM0hYTDlLS2J1S05SV3k4cVZrcFdySEdkeWRIY25QZl92
bFRZUUY3cjlGY1piRU5MeVNfRHN4cGNkbzBkb1ZnTi1hTXhkZVExTTJZdHNaazFSM0xGeDNOUVNB
aHFPa29VdzFCT2JGNjNDU1VPdDVKNXF5eGMyMlJ3OU8waUVWeDl5UWJmc1hnP3V0bV9zb3VyY2U9
Z20mdXRtX21lZGl1bT1lbWFpbCZhdXRvPXRydWU+dW5zdWJzY3JpYmUgLg0KDQpFdmVuIGlmIHlv
dSB1bnN1YnNjcmliZSBmcm9tIHRoZXNlIGVtYWlscywgeW914oCZbGwgY29udGludWUgdG8gcmVj
ZWl2ZSAgDQpzZWN1cml0eSBhbGVydHMuDQoNCsKpIDIwMjYgR29vZ2xlIExMQyAxNjAwIEFtcGhp
dGhlYXRyZSBQYXJrd2F5LCBNb3VudGFpbiBWaWV3LCBDQSA5NDA0Mw0K
--00000000000015913906592459b2
Content-Type: text/html; charset="UTF-8"
Content-Transfer-Encoding: quoted-printable

<!DOCTYPE html><html xmlns:v=3Durn:schemas-microsoft-com:vml xmlns:o=3Durn:=
schemas-microsoft-com:office:office lang=3Den><head>
<title></title><meta http-equiv=3DContent-Type content=3D"text/html; charse=
t=3Dutf-8"><meta name=3Dviewport content=3Dwidth=3Ddevice-width,initial-sca=
le=3D1><!--[if mso]>
<xml><w:WordDocument xmlns:w=3D"urn:schemas-microsoft-com:office:word"><w:D=
ontUseAdvancedTypographyReadingMail/></w:WordDocument>
<o:OfficeDocumentSettings><o:PixelsPerInch>96</o:PixelsPerInch><o:AllowPNG/=
></o:OfficeDocumentSettings></xml>
<![endif]--><!--[if !mso]><!--><link href=3Dhttps://fonts.googleapis.com/cs=
s?family=3DGoogle+Sans:400,500,600,700%7CRoboto:400,500,600,700;display=3Ds=
wap rel=3Dstylesheet type=3Dtext/css><link href=3Dhttps://fonts.googleapis.=
com/css?family=3DRoboto:400,500,600,700;display=3Dswap rel=3Dstylesheet typ=
e=3Dtext/css><!--<![endif]--><style>
*{box-sizing:border-box}body{margin:0;padding:0}a[x-apple-data-detectors]{c=
olor:inherit!important;text-decoration:inherit!important}#MessageViewBody a=
{color:inherit;text-decoration:none}p{line-height:inherit}.desktop_hide,.de=
sktop_hide table{mso-hide:all;display:none;max-height:0;overflow:hidden}.im=
age_block img+div{display:none}sub,sup{font-size:75%;line-height:0} @media =
(max-width:630px){.mobile_hide{display:none}.row-content{width:100%!importa=
nt}.stack .column{width:100%;display:block}.mobile_hide{min-height:0;max-he=
ight:0;max-width:0;overflow:hidden;font-size:0}.desktop_hide,.desktop_hide =
table{display:table!important;max-height:none!important}.row-2 .column-1 .b=
lock-1.paragraph_block td.pad{padding:3px 0!important}.row-10 .column-1 .bl=
ock-23.spacer_block{height:4px!important}.row-1 .column-1{padding:28px 18px=
 0!important}.row-2 .column-1{padding:20px 18px 8px!important}.row-3 .colum=
n-1{padding:12px 18px 3px!important}.row-4 .column-1{padding:29px 18px 0!im=
portant}.row-5 .column-1,.row-6 .column-1{padding:16px 18px 0!important}.ro=
w-11 .column-1{padding:16px 18px!important}.row-12 .column-1,.row-13 .colum=
n-1{padding:0 18px 16px!important}.row-16 .column-1{padding:0 18px!importan=
t}.row-17 .column-1{padding:8px 18px!important}}
</style><!--[if mso ]><style>sup, sub { font-size: 100% !important; } sup {=
 mso-text-raise:10% } sub { mso-text-raise:-10% }</style> <![endif]--><!--[=
if true]><style>.forceBgColor{background-color: white !important}</style><!=
[endif]--></head><body dir=3Dltr class=3D"body forceBgColor" style=3Dbackgr=
ound-color:transparent;margin:0;padding:0;-webkit-text-size-adjust:none;tex=
t-size-adjust:none><table class=3Dnl-container width=3D100% border=3D0 cell=
padding=3D0 cellspacing=3D0 role=3Dpresentation style=3Dmso-table-lspace:0;=
mso-table-rspace:0;background-color:transparent><tbody><tr><td><table class=
=3D"row row-1" align=3Dcenter width=3D100% border=3D0 cellpadding=3D0 cells=
pacing=3D0 role=3Dpresentation style=3Dmso-table-lspace:0;mso-table-rspace:=
0><tbody><tr><td><table class=3D"row-content stack" align=3Dcenter border=
=3D0 cellpadding=3D0 cellspacing=3D0 role=3Dpresentation style=3D"mso-table=
-lspace:0;mso-table-rspace:0;border-left:1px solid #e8eaed;border-right:1px=
 solid #e8eaed;color:#000;border-radius:8px 8px 0 0;border-top:1px solid #e=
8eaed;width:610px;margin:0 auto" width=3D610><tbody><tr><td class=3D"column=
 column-1" width=3D100% style=3Dmso-table-lspace:0;mso-table-rspace:0;font-=
weight:400;text-align:left;padding-left:40px;padding-right:40px;padding-top=
:28px;vertical-align:top><table class=3D"html_block block-1" width=3D100% b=
order=3D0 cellpadding=3D0 cellspacing=3D0 role=3Dpresentation style=3Dmso-t=
able-lspace:0;mso-table-rspace:0><tr><td class=3Dpad><div style=3D"font-fam=
ily:&#39;Google Sans&#39;,Roboto,arial,sans-serif;text-align:center" align=
=3Dcenter><img src=3Dhttps://www.gstatic.com/identity/boq/thirdpartyconnect=
ions/notification/40px_x4.png height=3D40></div></td></tr></table></td></tr=
></tbody></table></td></tr></tbody></table><table class=3D"row row-2" align=
=3Dcenter width=3D100% border=3D0 cellpadding=3D0 cellspacing=3D0 role=3Dpr=
esentation style=3Dmso-table-lspace:0;mso-table-rspace:0><tbody><tr><td><ta=
ble class=3D"row-content stack" align=3Dcenter border=3D0 cellpadding=3D0 c=
ellspacing=3D0 role=3Dpresentation style=3D"mso-table-lspace:0;mso-table-rs=
pace:0;border-left:1px solid #e8eaed;border-radius:0;border-right:1px solid=
 #e8eaed;color:#000;width:610px;margin:0 auto" width=3D610><tbody><tr><td c=
lass=3D"column column-1" width=3D100% style=3Dmso-table-lspace:0;mso-table-=
rspace:0;font-weight:400;text-align:left;padding-bottom:8px;padding-left:40=
px;padding-right:40px;padding-top:20px;vertical-align:top>
<table class=3D"paragraph_block block-1" width=3D100% border=3D0 cellpaddin=
g=3D0 cellspacing=3D0 role=3Dpresentation style=3Dmso-table-lspace:0;mso-ta=
ble-rspace:0;word-break:break-word><tr><td class=3Dpad style=3Dpadding-bott=
om:3px;padding-top:3px><div style=3D"color:#2c2c2c;direction:ltr;font-famil=
y:&#39;Google Sans&#39;,Roboto,arial,sans-serif;font-size:22px;font-weight:=
400;letter-spacing:0;line-height:1.2;text-align:center;mso-line-height-alt:=
26px"><p style=3Dmargin:0>
Keep track of your Google Account data</p></div></td></tr></table></td></tr=
></tbody></table></td></tr></tbody></table><table class=3D"row row-3" align=
=3Dcenter width=3D100% border=3D0 cellpadding=3D0 cellspacing=3D0 role=3Dpr=
esentation style=3Dmso-table-lspace:0;mso-table-rspace:0><tbody><tr><td><ta=
ble class=3D"row-content stack" align=3Dcenter border=3D0 cellpadding=3D0 c=
ellspacing=3D0 role=3Dpresentation style=3D"mso-table-lspace:0;mso-table-rs=
pace:0;border-left:1px solid #e8eaed;border-radius:0;border-right:1px solid=
 #e8eaed;color:#000;width:610px;margin:0 auto" width=3D610><tbody><tr><td c=
lass=3D"column column-1" width=3D100% style=3Dmso-table-lspace:0;mso-table-=
rspace:0;font-weight:400;text-align:left;padding-bottom:3px;padding-left:40=
px;padding-right:40px;padding-top:12px;vertical-align:top><table class=3D"h=
tml_block block-1" width=3D100% border=3D0 cellpadding=3D0 cellspacing=3D0 =
role=3Dpresentation style=3Dmso-table-lspace:0;mso-table-rspace:0><tr><td c=
lass=3Dpad><div style=3D"font-family:&#39;Google Sans&#39;,Roboto,arial,san=
s-serif;text-align:center" align=3Dcenter><table role=3Dpresentation cellsp=
acing=3D0 cellpadding=3D0 border=3D0 width=3D100%>
  <tr>
    <td align=3Dcenter>
      <table role=3Dpresentation cellspacing=3D0 cellpadding=3D0 border=3D0=
>
        <tr>
          <td style=3D"vertical-align: middle; padding: 0px 4px 0px 4px; li=
ne-height: 20px;">
              <img src=3Dhttps://lh3.googleusercontent.com/a/ACg8ocJrhPBpmU=
K_IFDl8noxrOXR7QlTa0_gnVg4FxAiIS38TMV9Uw=3Ds512-mo width=3D24 height=3D24 s=
tyle=3D"display: block; border: 0; border-radius: 50%;">
          </td>
          <td style=3D"vertical-align: middle; padding: 0px 4px 0px 4px; li=
ne-height: 20px; font-size: 14px; color: #1f1f1f;">
            <a style=3D"font-weight:500; color: inherit; text-decoration: n=
one; cursor: default;">
              violetprouses@gmail.com
            </a>
          </td>
        </tr>
      </table>
    </td>
  </tr>
</table></div></td></tr></table></td></tr></tbody></table></td></tr></tbody=
></table><table class=3D"row row-4" align=3Dcenter width=3D100% border=3D0 =
cellpadding=3D0 cellspacing=3D0 role=3Dpresentation style=3Dmso-table-lspac=
e:0;mso-table-rspace:0><tbody><tr><td><table class=3D"row-content stack" al=
ign=3Dcenter border=3D0 cellpadding=3D0 cellspacing=3D0 role=3Dpresentation=
 style=3D"mso-table-lspace:0;mso-table-rspace:0;border-left:1px solid #e8ea=
ed;border-radius:0;border-right:1px solid #e8eaed;color:#000;width:610px;ma=
rgin:0 auto" width=3D610><tbody><tr><td class=3D"column column-1" width=3D1=
00% style=3Dmso-table-lspace:0;mso-table-rspace:0;font-weight:400;text-alig=
n:left;padding-left:40px;padding-right:40px;padding-top:29px;vertical-align=
:top><table class=3D"divider_block block-1" width=3D100% border=3D0 cellpad=
ding=3D0 cellspacing=3D0 role=3Dpresentation style=3Dmso-table-lspace:0;mso=
-table-rspace:0><tr><td class=3Dpad><div class=3Dalignment align=3Dcenter><=
table border=3D0 cellpadding=3D0 cellspacing=3D0 role=3Dpresentation width=
=3D100% style=3Dmso-table-lspace:0;mso-table-rspace:0><tr><td class=3Ddivid=
er_inner style=3D"font-size:1px;line-height:1px;border-top:1px solid #dadce=
0"><span style=3D"word-break: break-word;">=E2=80=8A</span></td></tr></tabl=
e></div></td></tr></table>
</td></tr></tbody></table></td></tr></tbody></table><table class=3D"row row=
-5 mobile_hide" align=3Dcenter width=3D100% border=3D0 cellpadding=3D0 cell=
spacing=3D0 role=3Dpresentation style=3Dmso-table-lspace:0;mso-table-rspace=
:0><tbody><tr><td><table class=3D"row-content stack" align=3Dcenter border=
=3D0 cellpadding=3D0 cellspacing=3D0 role=3Dpresentation style=3D"mso-table=
-lspace:0;mso-table-rspace:0;border-left:1px solid #e8eaed;border-radius:0;=
border-right:1px solid #e8eaed;color:#000;width:610px;margin:0 auto" width=
=3D610><tbody><tr><td class=3D"column column-1" width=3D100% style=3Dmso-ta=
ble-lspace:0;mso-table-rspace:0;font-weight:400;text-align:left;padding-lef=
t:40px;padding-right:40px;padding-top:16px;vertical-align:top><table class=
=3D"html_block block-1" width=3D100% border=3D0 cellpadding=3D0 cellspacing=
=3D0 role=3Dpresentation style=3Dmso-table-lspace:0;mso-table-rspace:0><tr>=
<td class=3Dpad><div style=3D"font-family:&#39;Google Sans&#39;,Roboto,aria=
l,sans-serif;text-align:center" align=3Dcenter><img src=3Dhttps://www.gstat=
ic.com/identity/boq/thirdpartyconnections/notification/r_illustration_x4.pn=
g width=3D60%></div></td></tr></table></td></tr></tbody></table></td></tr><=
/tbody></table><!--[if !mso]><!--><table class=3D"row row-6 desktop_hide" a=
lign=3Dcenter width=3D100% border=3D0 cellpadding=3D0 cellspacing=3D0 role=
=3Dpresentation style=3Dmso-table-lspace:0;mso-table-rspace:0;mso-hide:all;=
display:none;max-height:0;overflow:hidden><tbody><tr><td><table class=3D"ro=
w-content stack" align=3Dcenter border=3D0 cellpadding=3D0 cellspacing=3D0 =
role=3Dpresentation style=3D"mso-table-lspace:0;mso-table-rspace:0;mso-hide=
:all;display:none;max-height:0;overflow:hidden;border-left:1px solid #e8eae=
d;border-radius:0;border-right:1px solid #e8eaed;color:#000;width:610px;mar=
gin:0 auto" width=3D610><tbody><tr><td class=3D"column column-1" width=3D10=
0% style=3Dmso-table-lspace:0;mso-table-rspace:0;font-weight:400;text-align=
:left;padding-left:40px;padding-right:40px;padding-top:16px;vertical-align:=
top><table class=3D"html_block block-1" width=3D100% border=3D0 cellpadding=
=3D0 cellspacing=3D0 role=3Dpresentation style=3Dmso-table-lspace:0;mso-tab=
le-rspace:0;mso-hide:all;display:none;max-height:0;overflow:hidden><tr><td =
class=3Dpad><div style=3D"font-family:&#39;Google Sans&#39;,Roboto,arial,sa=
ns-serif;text-align:center" align=3Dcenter>
<!--[if false]><!--><img src=3Dhttps://www.gstatic.com/identity/boq/thirdpa=
rtyconnections/notification/r_illustration_x4.png width=3D100%><!--<![endif=
]--></div></td></tr></table></td></tr></tbody></table></td></tr></tbody></t=
able><!--<![endif]--><table class=3D"row row-7 mobile_hide" align=3Dcenter =
width=3D100% border=3D0 cellpadding=3D0 cellspacing=3D0 role=3Dpresentation=
 style=3Dmso-table-lspace:0;mso-table-rspace:0><tbody><tr><td><table class=
=3D"row-content stack" align=3Dcenter border=3D0 cellpadding=3D0 cellspacin=
g=3D0 role=3Dpresentation style=3D"mso-table-lspace:0;mso-table-rspace:0;bo=
rder-left:1px solid #e8eaed;border-radius:0;border-right:1px solid #e8eaed;=
color:#000;width:610px;margin:0 auto" width=3D610><tbody><tr><td class=3D"c=
olumn column-1" width=3D100% style=3Dmso-table-lspace:0;mso-table-rspace:0;=
font-weight:400;text-align:left;vertical-align:top><table class=3D"html_blo=
ck block-1" width=3D100% border=3D0 cellpadding=3D0 cellspacing=3D0 role=3D=
presentation style=3Dmso-table-lspace:0;mso-table-rspace:0><tr><td class=3D=
pad>
<div style=3D"font-family:&#39;Google Sans&#39;,Roboto,arial,sans-serif;tex=
t-align:center" align=3Dcenter></div></td></tr></table><table class=3D"html=
_block block-6" width=3D100% border=3D0 cellpadding=3D0 cellspacing=3D0 rol=
e=3Dpresentation style=3Dmso-table-lspace:0;mso-table-rspace:0><tr><td clas=
s=3Dpad><div style=3D"font-family:&#39;Google Sans&#39;,Roboto,arial,sans-s=
erif;text-align:center" align=3Dcenter><table cellspacing=3D0 cellpadding=
=3D0 border=3D0 width=3D100% style=3D"background-color: transparent;">
  <tr>
    <td align=3Dcenter style=3D"padding: 16px 40px;">
      <table cellspacing=3D0 cellpadding=3D0 border=3D0 width=3D100% style=
=3D"background-color: #d3e3fd; border-radius: 12px; border: 1px solid trans=
parent;">
        <tr>
          <td style=3D"padding-left: 8px; padding-right: 8px;">
            <table cellspacing=3D0 cellpadding=3D0 border=3D0 width=3D100%>
              <tr>
                <td style=3D"vertical-align: top; padding-left: 8px; paddin=
g-right: 8px;">
                  <p>
                    <img src=3Dhttps://www.gstatic.com/identity/boq/thirdpa=
rtyconnections/notification/info_24px_x4.png height=3D24>
                  </p>
                </td>
                <td style=3D"vertical-align: top; padding-left: 8px; paddin=
g-right: 8px; color: #041E49; font-size: 14px; font-weight: 400;">
                  <p style=3D"line-height: 20px; margin-bottom: 8px;">
                    You&#39;re receiving this email because you used Sign i=
n with Google to sign in to
                      <span style=3D"font-weight: 700; text-decoration-line=
: underline; text-decoration-style: solid; text-decoration-skip-ink: auto; =
text-decoration-thickness: auto; text-underline-offset: auto; text-underlin=
e-position: from-font;">
                        <a href=3Dhttps://c.gle/AKMee0dPPsatg6AyQQM3F-wYI9R=
Vjxtkn1Q9jsJJmcsWPRO6w3i_eivh_1Zg0AYdfqMExQFdUzHAskiKVslIkqp93AdUgR8RpEiufc=
ElZTfNKojfLPdNqlW6xTyMmIBBvlYg7z5BCfkAdA style=3D"color: #041E49;">ecosia.o=
rg</a></span>
                    on <span style=3D"font-weight: 700;">August 16 at 6:41=
=E2=80=AFAM GMT+0</span>.
                  </p>
                  <p style=3D"line-height: 20px;">
                    This email summarizes the info you shared. There=E2=80=
=99s nothing you need to do right now.
                  </p>
                </td>
              </tr>
            </table>
          </td>
        </tr>
      </table>
    </td>
  </tr>
</table></div></td></tr></table><table class=3D"html_block block-7" width=
=3D100% border=3D0 cellpadding=3D0 cellspacing=3D0 role=3Dpresentation styl=
e=3Dmso-table-lspace:0;mso-table-rspace:0><tr><td class=3Dpad><div style=3D=
"font-family:&#39;Google Sans&#39;,Roboto,arial,sans-serif;text-align:cente=
r" align=3Dcenter></div></td></tr></table></td></tr></tbody></table></td></=
tr></tbody></table><!--[if !mso]><!--><table class=3D"row row-8 desktop_hid=
e" align=3Dcenter width=3D100% border=3D0 cellpadding=3D0 cellspacing=3D0 r=
ole=3Dpresentation style=3Dmso-table-lspace:0;mso-table-rspace:0;mso-hide:a=
ll;display:none;max-height:0;overflow:hidden><tbody><tr><td><table class=3D=
"row-content stack" align=3Dcenter border=3D0 cellpadding=3D0 cellspacing=
=3D0 role=3Dpresentation style=3D"mso-table-lspace:0;mso-table-rspace:0;mso=
-hide:all;display:none;max-height:0;overflow:hidden;border-left:1px solid #=
e8eaed;border-radius:0;border-right:1px solid #e8eaed;color:#000;width:610p=
x;margin:0 auto" width=3D610><tbody><tr><td class=3D"column column-1" width=
=3D100% style=3Dmso-table-lspace:0;mso-table-rspace:0;font-weight:400;text-=
align:left;vertical-align:top><table class=3D"html_block block-1" width=3D1=
00% border=3D0 cellpadding=3D0 cellspacing=3D0 role=3Dpresentation style=3D=
mso-table-lspace:0;mso-table-rspace:0;mso-hide:all;display:none;max-height:=
0;overflow:hidden><tr><td class=3Dpad><div style=3D"font-family:&#39;Google=
 Sans&#39;,Roboto,arial,sans-serif;text-align:center" align=3Dcenter><!--[i=
f false]><!--><!--<![endif]--></div></td></tr></table><table class=3D"html_=
block block-6" width=3D100% border=3D0 cellpadding=3D0 cellspacing=3D0 role=
=3Dpresentation style=3Dmso-table-lspace:0;mso-table-rspace:0;mso-hide:all;=
display:none;max-height:0;overflow:hidden><tr><td class=3Dpad><div style=3D=
"font-family:&#39;Google Sans&#39;,Roboto,arial,sans-serif;text-align:cente=
r" align=3Dcenter><!--[if false]><!--><table cellspacing=3D0 cellpadding=3D=
0 border=3D0 width=3D100% style=3D"background-color: transparent;">
  <tr>
    <td align=3Dcenter style=3D"padding: 16px 18px;">
      <table cellspacing=3D0 cellpadding=3D0 border=3D0 width=3D100% style=
=3D"background-color: #d3e3fd; border-radius: 12px; border: 1px solid trans=
parent;">
        <tr>
          <td style=3D"padding-left: 8px; padding-right: 8px;">
            <table cellspacing=3D0 cellpadding=3D0 border=3D0 width=3D100%>
              <tr>
                <td style=3D"vertical-align: top; padding-left: 8px; paddin=
g-right: 8px;">
                  <p>
                    <img src=3Dhttps://www.gstatic.com/identity/boq/thirdpa=
rtyconnections/notification/info_24px_x4.png height=3D24>
                  </p>
                </td>
                <td style=3D"vertical-align: top; padding-left: 8px; paddin=
g-right: 8px; color: #041E49; font-size: 14px; font-weight: 400;">
                  <p style=3D"line-height: 20px; margin-bottom: 8px;">
                    You&#39;re receiving this email because you used Sign i=
n with Google to sign in to
                      <span style=3D"font-weight: 700; text-decoration-line=
: underline; text-decoration-style: solid; text-decoration-skip-ink: auto; =
text-decoration-thickness: auto; text-underline-offset: auto; text-underlin=
e-position: from-font;">
                        <a href=3Dhttps://c.gle/AKMee0dPPsatg6AyQQM3F-wYI9R=
Vjxtkn1Q9jsJJmcsWPRO6w3i_eivh_1Zg0AYdfqMExQFdUzHAskiKVslIkqp93AdUgR8RpEiufc=
ElZTfNKojfLPdNqlW6xTyMmIBBvlYg7z5BCfkAdA style=3D"color: #041E49;">ecosia.o=
rg</a></span>
                    on <span style=3D"font-weight: 700;">August 16 at 6:41=
=E2=80=AFAM GMT+0</span>.
                  </p>
                  <p style=3D"line-height: 20px;">
                    This email summarizes the info you shared. There=E2=80=
=99s nothing you need to do right now.
                  </p>
                </td>
              </tr>
            </table>
          </td>
        </tr>
      </table>
    </td>
  </tr>
</table><!--<![endif]--></div></td></tr></table><table class=3D"html_block =
block-7" width=3D100% border=3D0 cellpadding=3D0 cellspacing=3D0 role=3Dpre=
sentation style=3Dmso-table-lspace:0;mso-table-rspace:0;mso-hide:all;displa=
y:none;max-height:0;overflow:hidden><tr><td class=3Dpad><div style=3D"font-=
family:&#39;Google Sans&#39;,Roboto,arial,sans-serif;text-align:center" ali=
gn=3Dcenter><!--[if false]><!--><!--<![endif]--></div></td></tr></table></t=
d></tr></tbody></table></td></tr></tbody></table><!--<![endif]--><table cla=
ss=3D"row row-9 mobile_hide" align=3Dcenter width=3D100% border=3D0 cellpad=
ding=3D0 cellspacing=3D0 role=3Dpresentation style=3Dmso-table-lspace:0;mso=
-table-rspace:0><tbody><tr><td><table class=3D"row-content stack" align=3Dc=
enter border=3D0 cellpadding=3D0 cellspacing=3D0 role=3Dpresentation style=
=3D"mso-table-lspace:0;mso-table-rspace:0;border-left:1px solid #e8eaed;bor=
der-radius:0;border-right:1px solid #e8eaed;color:#000;width:610px;margin:0=
 auto" width=3D610><tbody><tr><td class=3D"column column-1" width=3D100% st=
yle=3Dmso-table-lspace:0;mso-table-rspace:0;font-weight:400;text-align:left=
;vertical-align:top><table class=3D"html_block block-1" width=3D100% border=
=3D0 cellpadding=3D0 cellspacing=3D0 role=3Dpresentation style=3Dmso-table-=
lspace:0;mso-table-rspace:0><tr><td class=3Dpad><div style=3D"font-family:&=
#39;Google Sans&#39;,Roboto,arial,sans-serif;text-align:center" align=3Dcen=
ter></div></td></tr></table><table class=3D"html_block block-2" width=3D100=
% border=3D0 cellpadding=3D0 cellspacing=3D0 role=3Dpresentation style=3Dms=
o-table-lspace:0;mso-table-rspace:0><tr><td class=3Dpad><div style=3D"font-=
family:&#39;Google Sans&#39;,Roboto,arial,sans-serif;text-align:center" ali=
gn=3Dcenter><table cellspacing=3D0 cellpadding=3D0 border=3D0 width=3D100% =
style=3D"background-color: transparent;">
  <tr>
    <td align=3Dcenter style=3D"padding: 16px 40px 0px 40px;">
      <table cellspacing=3D0 cellpadding=3D0 border=3D0 width=3D100% style=
=3D"background-color: #F8FAFD; border-radius: 28px 28px 0px 0px; border-sty=
le: solid; border-width: 1px; border-color: transparent;">
        <tr>
          <td style=3D"padding: 16px 32px 0px 32px;">
            <table cellspacing=3D0 cellpadding=3D0 border=3D0 width=3D100%>
              <tr>
                <td style=3D"vertical-align: top; padding-top: 10px; paddin=
g-bottom: 10px; color: #202124; font-size: 14px; line-height: 20px; letter-=
spacing: 0.25px;">
                  <a style=3D"font-weight:500; color: #202124; text-decorat=
ion: none; cursor: default;">
                    ecosia.org received this profile info
                  </a>
                </td>
              </tr>
            </table>
          </td>
        </tr>
      </table>
    </td>
  </tr>
</table></div></td></tr></table><table class=3D"html_block block-3" width=
=3D100% border=3D0 cellpadding=3D0 cellspacing=3D0 role=3Dpresentation styl=
e=3Dmso-table-lspace:0;mso-table-rspace:0><tr><td class=3Dpad><div style=3D=
"font-family:&#39;Google Sans&#39;,Roboto,arial,sans-serif;text-align:cente=
r" align=3Dcenter></div></td></tr></table><table class=3D"html_block block-=
6" width=3D100% border=3D0 cellpadding=3D0 cellspacing=3D0 role=3Dpresentat=
ion style=3Dmso-table-lspace:0;mso-table-rspace:0><tr><td class=3Dpad><div =
style=3D"font-family:&#39;Google Sans&#39;,Roboto,arial,sans-serif;text-ali=
gn:center" align=3Dcenter></div></td></tr></table><table class=3D"html_bloc=
k block-7" width=3D100% border=3D0 cellpadding=3D0 cellspacing=3D0 role=3Dp=
resentation style=3Dmso-table-lspace:0;mso-table-rspace:0><tr><td class=3Dp=
ad><div style=3D"font-family:&#39;Google Sans&#39;,Roboto,arial,sans-serif;=
text-align:center" align=3Dcenter><table cellspacing=3D0 cellpadding=3D0 bo=
rder=3D0 width=3D100% style=3D"background-color: transparent;">
  <tr>
    <td align=3Dcenter style=3D"padding: 0px 40px;">
      <table cellspacing=3D0 cellpadding=3D0 border=3D0 width=3D100% style=
=3D"background-color: #F8FAFD; border-style: solid; border-width: 1px; bord=
er-color: transparent;">
        <tr>
          <td style=3D"padding: 0px 26px;">
            <table cellspacing=3D0 cellpadding=3D0 border=3D0 width=3D100%>
              <tr>
                <td style=3D"width: 10%; vertical-align: top; padding-top: =
10px; padding-bottom: 8px; padding-left: 6px; padding-right: 6px;">
                  <img src=3Dhttps://www.gstatic.com/identity/boq/thirdpart=
yconnections/notification/id_profile_x4.png width=3D24>
                </td>
                <td style=3D"vertical-align: top; padding-top: 8px; padding=
-bottom: 8px; padding-left: 6px; padding-right: 6px; font-weight: 400;">
                  <table cellspacing=3D0 cellpadding=3D0 border=3D0 width=
=3D100%>
                    <tr>
                      <td style=3D"color: #1f1f1f; font-size: 14px; line-he=
ight: 24px;">
                        violet smith
                      </td>
                    </tr>
                    <tr>
                      <td style=3D"color: #444746; font-size: 12px; line-he=
ight: 20px;">
                        Name and profile picture
                      </td>
                    </tr>
                  </table>
                </td>
              </tr>
            </table>
          </td>
        </tr>
      </table>
    </td>
  </tr>
</table></div></td></tr></table><table class=3D"html_block block-8" width=
=3D100% border=3D0 cellpadding=3D0 cellspacing=3D0 role=3Dpresentation styl=
e=3Dmso-table-lspace:0;mso-table-rspace:0><tr><td class=3Dpad><div style=3D=
"font-family:&#39;Google Sans&#39;,Roboto,arial,sans-serif;text-align:cente=
r" align=3Dcenter></div></td></tr></table><table class=3D"html_block block-=
9" width=3D100% border=3D0 cellpadding=3D0 cellspacing=3D0 role=3Dpresentat=
ion style=3Dmso-table-lspace:0;mso-table-rspace:0><tr><td class=3Dpad><div =
style=3D"font-family:&#39;Google Sans&#39;,Roboto,arial,sans-serif;text-ali=
gn:center" align=3Dcenter></div></td></tr></table><table class=3D"html_bloc=
k block-10" width=3D100% border=3D0 cellpadding=3D0 cellspacing=3D0 role=3D=
presentation style=3Dmso-table-lspace:0;mso-table-rspace:0><tr><td class=3D=
pad><div style=3D"font-family:&#39;Google Sans&#39;,Roboto,arial,sans-serif=
;text-align:center" align=3Dcenter><table cellspacing=3D0 cellpadding=3D0 b=
order=3D0 width=3D100% style=3D"background-color: transparent;">
  <tr>
    <td align=3Dcenter style=3D"padding: 0px 40px;">
      <table cellspacing=3D0 cellpadding=3D0 border=3D0 width=3D100% style=
=3D"background-color: #F8FAFD; border-style: solid; border-width: 1px; bord=
er-color: transparent;">
        <tr>
          <td style=3D"padding: 0px 26px;">
            <table cellspacing=3D0 cellpadding=3D0 border=3D0 width=3D100%>
              <tr>
                <td style=3D"width: 10%; vertical-align: top; padding-top: =
10px; padding-bottom: 8px; padding-left: 6px; padding-right: 6px;">
                  <img src=3Dhttps://www.gstatic.com/identity/boq/thirdpart=
yconnections/notification/id_email_x4.png width=3D24>
                </td>
                <td style=3D"vertical-align: top; padding-top: 8px; padding=
-bottom: 8px; padding-left: 6px; padding-right: 6px; font-weight: 400;">
                  <table cellspacing=3D0 cellpadding=3D0 border=3D0 width=
=3D100%>
                    <tr>
                      <td style=3D"color: #1f1f1f; font-size: 14px; line-he=
ight: 24px;">
                        <a style=3D"color: inherit; text-decoration: none; =
cursor: default;">
                          violetprouses@gmail.com
                        </a>
                      </td>
                    </tr>
                    <tr>
                      <td style=3D"color: #444746; font-size: 12px; line-he=
ight: 20px;">
                        Email address
                      </td>
                    </tr>
                  </table>
                </td>
              </tr>
            </table>
          </td>
        </tr>
      </table>
    </td>
  </tr>
</table></div></td></tr></table><table class=3D"html_block block-11" width=
=3D100% border=3D0 cellpadding=3D0 cellspacing=3D0 role=3Dpresentation styl=
e=3Dmso-table-lspace:0;mso-table-rspace:0><tr><td class=3Dpad><div style=3D=
"font-family:&#39;Google Sans&#39;,Roboto,arial,sans-serif;text-align:cente=
r" align=3Dcenter></div></td></tr></table><table class=3D"html_block block-=
12" width=3D100% border=3D0 cellpadding=3D0 cellspacing=3D0 role=3Dpresenta=
tion style=3Dmso-table-lspace:0;mso-table-rspace:0><tr><td class=3Dpad><div=
 style=3D"font-family:&#39;Google Sans&#39;,Roboto,arial,sans-serif;text-al=
ign:center" align=3Dcenter></div></td></tr></table><table class=3D"html_blo=
ck block-15" width=3D100% border=3D0 cellpadding=3D0 cellspacing=3D0 role=
=3Dpresentation style=3Dmso-table-lspace:0;mso-table-rspace:0><tr><td class=
=3Dpad><div style=3D"font-family:&#39;Google Sans&#39;,Roboto,arial,sans-se=
rif;text-align:center" align=3Dcenter></div></td></tr></table><table class=
=3D"html_block block-19" width=3D100% border=3D0 cellpadding=3D0 cellspacin=
g=3D0 role=3Dpresentation style=3Dmso-table-lspace:0;mso-table-rspace:0><tr=
><td class=3Dpad><div style=3D"font-family:&#39;Google Sans&#39;,Roboto,ari=
al,sans-serif;text-align:center" align=3Dcenter></div></td></tr></table><ta=
ble class=3D"html_block block-22" width=3D100% border=3D0 cellpadding=3D0 c=
ellspacing=3D0 role=3Dpresentation style=3Dmso-table-lspace:0;mso-table-rsp=
ace:0><tr><td class=3Dpad><div style=3D"font-family:&#39;Google Sans&#39;,R=
oboto,arial,sans-serif;text-align:center" align=3Dcenter><table cellspacing=
=3D0 cellpadding=3D0 border=3D0 width=3D100% style=3D"background-color: tra=
nsparent;">
  <tr>
    <td align=3Dcenter style=3D"padding: 0px 40px;">
      <table cellspacing=3D0 cellpadding=3D0 border=3D0 width=3D100% style=
=3D"background-color: #F8FAFD; border-style: solid; border-width: 1px; bord=
er-radius: 0px 0px 4px 4px; border-color: transparent;">
        <tr>
          <td style=3D"padding: 0px 32px 16px 32px;">
          </td>
        </tr>
      </table>
    </td>
  </tr>
</table></div></td></tr></table><div class=3D"spacer_block block-23" style=
=3Dheight:4px;line-height:4px;font-size:1px>=E2=80=8A</div><table class=3D"=
html_block block-24" width=3D100% border=3D0 cellpadding=3D0 cellspacing=3D=
0 role=3Dpresentation style=3Dmso-table-lspace:0;mso-table-rspace:0><tr><td=
 class=3Dpad><div style=3D"font-family:&#39;Google Sans&#39;,Roboto,arial,s=
ans-serif;text-align:center" align=3Dcenter></div></td></tr></table><table =
class=3D"html_block block-31" width=3D100% border=3D0 cellpadding=3D0 cells=
pacing=3D0 role=3Dpresentation style=3Dmso-table-lspace:0;mso-table-rspace:=
0><tr><td class=3Dpad><div style=3D"font-family:&#39;Google Sans&#39;,Robot=
o,arial,sans-serif;text-align:center" align=3Dcenter><table cellspacing=3D0=
 cellpadding=3D0 border=3D0 width=3D100% style=3D"background-color: transpa=
rent;">
  <tr>
    <td align=3Dcenter style=3D"padding: 0px 40px 32px 40px;">
      <table cellspacing=3D0 cellpadding=3D0 border=3D0 width=3D100% style=
=3D"background-color: #F8FAFD; border-radius: 4px 4px 28px 28px; border: 1p=
x solid transparent;">
        <tr>
          <td style=3D"padding: 16px 32px;">
            <table cellspacing=3D0 cellpadding=3D0 border=3D0 width=3D100%>
              <tr>
                <td style=3D"vertical-align: top; color: #3C4043; font-size=
: 14px; font-weight: 400; line-height: 20px;">
                  This email includes the info you shared on
                  <span style=3D"font-weight: 700;">August 16 at 6:41=E2=80=
=AFAM GMT+0</span>
                </td>
              </tr>
            </table>
          </td>
        </tr>
      </table>
    </td>
  </tr>
</table>
</div></td></tr></table><table class=3D"html_block block-32" width=3D100% b=
order=3D0 cellpadding=3D0 cellspacing=3D0 role=3Dpresentation style=3Dmso-t=
able-lspace:0;mso-table-rspace:0><tr><td class=3Dpad><div style=3D"font-fam=
ily:&#39;Google Sans&#39;,Roboto,arial,sans-serif;text-align:center" align=
=3Dcenter><div style=3D"vertical-align: top; text-align: start; padding-lef=
t: 40px; padding-right: 40px; font-weight: 400; font-size: 14px; color: #3c=
4043; line-height: 20px; letter-spacing: 0.2px;">
  If you want to stop using Sign in with Google with
  <a style=3D"color: inherit; text-decoration: none; cursor: default;">
    ecosia.org</a>, go to your Google Account.
</div></div></td></tr></table><table class=3D"html_block block-33" width=3D=
100% border=3D0 cellpadding=3D0 cellspacing=3D0 role=3Dpresentation style=
=3Dmso-table-lspace:0;mso-table-rspace:0>
<tr><td class=3Dpad><div style=3D"font-family:&#39;Google Sans&#39;,Roboto,=
arial,sans-serif;text-align:center" align=3Dcenter></div></td></tr></table>=
</td></tr></tbody></table></td></tr></tbody></table><!--[if !mso]><!--><tab=
le class=3D"row row-10 desktop_hide" align=3Dcenter width=3D100% border=3D0=
 cellpadding=3D0 cellspacing=3D0 role=3Dpresentation style=3Dmso-table-lspa=
ce:0;mso-table-rspace:0;mso-hide:all;display:none;max-height:0;overflow:hid=
den><tbody><tr><td><table class=3D"row-content stack" align=3Dcenter border=
=3D0 cellpadding=3D0 cellspacing=3D0 role=3Dpresentation style=3D"mso-table=
-lspace:0;mso-table-rspace:0;mso-hide:all;display:none;max-height:0;overflo=
w:hidden;border-left:1px solid #e8eaed;border-radius:0;border-right:1px sol=
id #e8eaed;color:#000;width:610px;margin:0 auto" width=3D610><tbody><tr><td=
 class=3D"column column-1" width=3D100% style=3Dmso-table-lspace:0;mso-tabl=
e-rspace:0;font-weight:400;text-align:left;vertical-align:top><table class=
=3D"html_block block-1" width=3D100% border=3D0 cellpadding=3D0 cellspacing=
=3D0 role=3Dpresentation style=3Dmso-table-lspace:0;mso-table-rspace:0;mso-=
hide:all;display:none;max-height:0;overflow:hidden><tr><td class=3Dpad><div=
 style=3D"font-family:&#39;Google Sans&#39;,Roboto,arial,sans-serif;text-al=
ign:center" align=3Dcenter><!--[if false]><!--><!--<![endif]--></div></td><=
/tr></table><table class=3D"html_block block-2" width=3D100% border=3D0 cel=
lpadding=3D0 cellspacing=3D0 role=3Dpresentation style=3Dmso-table-lspace:0=
;mso-table-rspace:0;mso-hide:all;display:none;max-height:0;overflow:hidden>=
<tr><td class=3Dpad><div style=3D"font-family:&#39;Google Sans&#39;,Roboto,=
arial,sans-serif;text-align:center" align=3Dcenter><!--[if false]><!--><tab=
le cellspacing=3D0 cellpadding=3D0 border=3D0 width=3D100% style=3D"backgro=
und-color: transparent;">
  <tr>
    <td align=3Dcenter style=3D"padding: 16px 18px 0px 18px;">
      <table cellspacing=3D0 cellpadding=3D0 border=3D0 width=3D100% style=
=3D"background-color: #F8FAFD; border-radius: 28px 28px 0px 0px; border-sty=
le: solid; border-width: 1px; border-color: transparent;">
        <tr>
          <td style=3D"padding: 16px 32px 0px 32px;">
            <table cellspacing=3D0 cellpadding=3D0 border=3D0 width=3D100%>
              <tr>
                <td style=3D"vertical-align: top; padding-top: 10px; paddin=
g-bottom: 10px; color: #202124; font-size: 14px; line-height: 20px; letter-=
spacing: 0.25px;">
                  <a style=3D"font-weight:600; color: #202124; text-decorat=
ion: none; cursor: default;">
                    ecosia.org received this profile info
                  </a>
                </td>
              </tr>
            </table>
          </td>
        </tr>
      </table>
    </td>
  </tr>
</table><!--<![endif]--></div></td></tr></table><table class=3D"html_block =
block-3" width=3D100% border=3D0 cellpadding=3D0 cellspacing=3D0 role=3Dpre=
sentation style=3Dmso-table-lspace:0;mso-table-rspace:0;mso-hide:all;displa=
y:none;max-height:0;overflow:hidden><tr><td class=3Dpad><div style=3D"font-=
family:&#39;Google Sans&#39;,Roboto,arial,sans-serif;text-align:center" ali=
gn=3Dcenter><!--[if false]><!--><!--<![endif]--></div></td></tr></table><ta=
ble class=3D"html_block block-6" width=3D100% border=3D0 cellpadding=3D0 ce=
llspacing=3D0 role=3Dpresentation style=3Dmso-table-lspace:0;mso-table-rspa=
ce:0;mso-hide:all;display:none;max-height:0;overflow:hidden><tr><td class=
=3Dpad><div style=3D"font-family:&#39;Google Sans&#39;,Roboto,arial,sans-se=
rif;text-align:center" align=3Dcenter><!--[if false]><!--><!--<![endif]--><=
/div></td></tr></table><table class=3D"html_block block-7" width=3D100% bor=
der=3D0 cellpadding=3D0 cellspacing=3D0 role=3Dpresentation style=3Dmso-tab=
le-lspace:0;mso-table-rspace:0;mso-hide:all;display:none;max-height:0;overf=
low:hidden><tr><td class=3Dpad><div style=3D"font-family:&#39;Google Sans&#=
39;,Roboto,arial,sans-serif;text-align:center" align=3Dcenter><!--[if false=
]><!--><table cellspacing=3D0 cellpadding=3D0 border=3D0 width=3D100% style=
=3D"background-color: transparent;">
  <tr>
    <td align=3Dcenter style=3D"padding: 0px 18px;">
      <table cellspacing=3D0 cellpadding=3D0 border=3D0 width=3D100% style=
=3D"background-color: #F8FAFD; border-style: solid; border-width: 1px; bord=
er-color: transparent;">
        <tr>
          <td style=3D"padding: 0px 26px;">
            <table cellspacing=3D0 cellpadding=3D0 border=3D0 width=3D100%>
              <tr>
                <td style=3D"width: 10%; vertical-align: top; padding-top: =
10px; padding-bottom: 8px; padding-left: 6px; padding-right: 6px;">
                  <img src=3Dhttps://www.gstatic.com/identity/boq/thirdpart=
yconnections/notification/id_profile_x4.png width=3D24>
                </td>
                <td style=3D"vertical-align: top; padding-top: 8px; padding=
-bottom: 8px; padding-left: 6px; padding-right: 6px; font-weight: 400;">
                  <table cellspacing=3D0 cellpadding=3D0 border=3D0 width=
=3D100%>
                    <tr>
                      <td style=3D"color: #1f1f1f; font-size: 14px; line-he=
ight: 24px;">
                        violet smith
                      </td>
                    </tr>
                    <tr>
                      <td style=3D"color: #444746; font-size: 12px; line-he=
ight: 20px;">
                        Name and profile picture
                      </td>
                    </tr>
                  </table>
                </td>
              </tr>
            </table>
          </td>
        </tr>
      </table>
    </td>
  </tr>
</table><!--<![endif]--></div></td></tr></table><table class=3D"html_block =
block-8" width=3D100% border=3D0 cellpadding=3D0 cellspacing=3D0 role=3Dpre=
sentation style=3Dmso-table-lspace:0;mso-table-rspace:0;mso-hide:all;displa=
y:none;max-height:0;overflow:hidden><tr><td class=3Dpad><div style=3D"font-=
family:&#39;Google Sans&#39;,Roboto,arial,sans-serif;text-align:center" ali=
gn=3Dcenter><!--[if false]><!--><!--<![endif]--></div></td></tr></table><ta=
ble class=3D"html_block block-9" width=3D100% border=3D0 cellpadding=3D0 ce=
llspacing=3D0 role=3Dpresentation style=3Dmso-table-lspace:0;mso-table-rspa=
ce:0;mso-hide:all;display:none;max-height:0;overflow:hidden><tr><td class=
=3Dpad><div style=3D"font-family:&#39;Google Sans&#39;,Roboto,arial,sans-se=
rif;text-align:center" align=3Dcenter><!--[if false]><!--><!--<![endif]--><=
/div></td></tr></table><table class=3D"html_block block-10" width=3D100% bo=
rder=3D0 cellpadding=3D0 cellspacing=3D0 role=3Dpresentation style=3Dmso-ta=
ble-lspace:0;mso-table-rspace:0;mso-hide:all;display:none;max-height:0;over=
flow:hidden><tr><td class=3Dpad><div style=3D"font-family:&#39;Google Sans&=
#39;,Roboto,arial,sans-serif;text-align:center" align=3Dcenter><!--[if fals=
e]><!--><table cellspacing=3D0 cellpadding=3D0 border=3D0 width=3D100% styl=
e=3D"background-color: transparent;">
  <tr>
    <td align=3Dcenter style=3D"padding: 0px 18px;">
      <table cellspacing=3D0 cellpadding=3D0 border=3D0 width=3D100% style=
=3D"background-color: #F8FAFD; border-style: solid; border-width: 1px; bord=
er-color: transparent;">
        <tr>
          <td style=3D"padding: 0px 26px;">
            <table cellspacing=3D0 cellpadding=3D0 border=3D0 width=3D100%>
              <tr>
                <td style=3D"width: 10%; vertical-align: top; padding-top: =
10px; padding-bottom: 8px; padding-left: 6px; padding-right: 6px;">
                  <img src=3Dhttps://www.gstatic.com/identity/boq/thirdpart=
yconnections/notification/id_email_x4.png width=3D24>
                </td>
                <td style=3D"vertical-align: top; padding-top: 8px; padding=
-bottom: 8px; padding-left: 6px; padding-right: 6px; font-weight: 400;">
                  <table cellspacing=3D0 cellpadding=3D0 border=3D0 width=
=3D100%>
                    <tr>
                      <td style=3D"color: #1f1f1f; font-size: 14px; line-he=
ight: 24px;">
                        <a style=3D"color: inherit; text-decoration: none; =
cursor: default;">
                          violetprouses@gmail.com
                        </a>
                      </td>
                    </tr>
                    <tr>
                      <td style=3D"color: #444746; font-size: 12px; line-he=
ight: 20px;">
                        Email address
                      </td>
                    </tr>
                  </table>
                </td>
              </tr>
            </table>
          </td>
        </tr>
      </table>
    </td>
  </tr>
</table><!--<![endif]--></div></td></tr></table><table class=3D"html_block =
block-11" width=3D100% border=3D0 cellpadding=3D0 cellspacing=3D0 role=3Dpr=
esentation style=3Dmso-table-lspace:0;mso-table-rspace:0;mso-hide:all;displ=
ay:none;max-height:0;overflow:hidden><tr><td class=3Dpad><div style=3D"font=
-family:&#39;Google Sans&#39;,Roboto,arial,sans-serif;text-align:center" al=
ign=3Dcenter><!--[if false]><!--><!--<![endif]--></div></td></tr></table><t=
able class=3D"html_block block-12" width=3D100% border=3D0 cellpadding=3D0 =
cellspacing=3D0 role=3Dpresentation style=3Dmso-table-lspace:0;mso-table-rs=
pace:0;mso-hide:all;display:none;max-height:0;overflow:hidden><tr><td class=
=3Dpad><div style=3D"font-family:&#39;Google Sans&#39;,Roboto,arial,sans-se=
rif;text-align:center" align=3Dcenter><!--[if false]><!--><!--<![endif]--><=
/div></td></tr></table><table class=3D"html_block block-15" width=3D100% bo=
rder=3D0 cellpadding=3D0 cellspacing=3D0 role=3Dpresentation style=3Dmso-ta=
ble-lspace:0;mso-table-rspace:0;mso-hide:all;display:none;max-height:0;over=
flow:hidden><tr><td class=3Dpad><div style=3D"font-family:&#39;Google Sans&=
#39;,Roboto,arial,sans-serif;text-align:center" align=3Dcenter><!--[if fals=
e]><!--><!--<![endif]--></div></td></tr></table><table class=3D"html_block =
block-19" width=3D100% border=3D0 cellpadding=3D0 cellspacing=3D0 role=3Dpr=
esentation style=3Dmso-table-lspace:0;mso-table-rspace:0;mso-hide:all;displ=
ay:none;max-height:0;overflow:hidden><tr><td class=3Dpad><div style=3D"font=
-family:&#39;Google Sans&#39;,Roboto,arial,sans-serif;text-align:center" al=
ign=3Dcenter><!--[if false]><!--><!--<![endif]--></div></td></tr></table><t=
able class=3D"html_block block-22" width=3D100% border=3D0 cellpadding=3D0 =
cellspacing=3D0 role=3Dpresentation style=3Dmso-table-lspace:0;mso-table-rs=
pace:0;mso-hide:all;display:none;max-height:0;overflow:hidden><tr><td class=
=3Dpad><div style=3D"font-family:&#39;Google Sans&#39;,Roboto,arial,sans-se=
rif;text-align:center" align=3Dcenter><!--[if false]><!--><table cellspacin=
g=3D0 cellpadding=3D0 border=3D0 width=3D100% style=3D"background-color: tr=
ansparent;">
  <tr>
    <td align=3Dcenter style=3D"padding: 0px 18px;">
      <table cellspacing=3D0 cellpadding=3D0 border=3D0 width=3D100% style=
=3D"background-color: #F8FAFD; border-style: solid; border-width: 1px; bord=
er-radius: 0px 0px 4px 4px; border-color: transparent;">
        <tr>
          <td style=3D"padding: 0px 32px 16px 32px;">
          </td>
        </tr>
      </table>
    </td>
  </tr>
</table><!--<![endif]--></div></td></tr></table><div class=3D"spacer_block =
block-23" style=3Dheight:4px;line-height:4px;font-size:1px>=E2=80=8A</div><=
table class=3D"html_block block-24" width=3D100% border=3D0 cellpadding=3D0=
 cellspacing=3D0 role=3Dpresentation style=3Dmso-table-lspace:0;mso-table-r=
space:0;mso-hide:all;display:none;max-height:0;overflow:hidden><tr><td clas=
s=3Dpad><div style=3D"font-family:&#39;Google Sans&#39;,Roboto,arial,sans-s=
erif;text-align:center" align=3Dcenter><!--[if false]><!--><!--<![endif]-->=
</div></td></tr>
</table><table class=3D"html_block block-31" width=3D100% border=3D0 cellpa=
dding=3D0 cellspacing=3D0 role=3Dpresentation style=3Dmso-table-lspace:0;ms=
o-table-rspace:0;mso-hide:all;display:none;max-height:0;overflow:hidden><tr=
><td class=3Dpad><div style=3D"font-family:&#39;Google Sans&#39;,Roboto,ari=
al,sans-serif;text-align:center" align=3Dcenter><!--[if false]><!--><table =
cellspacing=3D0 cellpadding=3D0 border=3D0 width=3D100% style=3D"background=
-color: transparent;">
  <tr>
    <td align=3Dcenter style=3D"padding: 0px 18px 32px 18px;">
      <table cellspacing=3D0 cellpadding=3D0 border=3D0 width=3D100% style=
=3D"background-color: #F8FAFD; border-radius: 4px 4px 28px 28px; border: 1p=
x solid transparent;">
        <tr>
          <td style=3D"padding: 16px 32px;">
            <table cellspacing=3D0 cellpadding=3D0 border=3D0 width=3D100%>
              <tr>
                <td style=3D"vertical-align: top; color: #3C4043; font-size=
: 14px; font-weight: 400; line-height: 20px;">
                  This email includes the info you shared on
                  <span style=3D"font-weight: 700;">August 16 at 6:41=E2=80=
=AFAM GMT+0</span>
                </td>
              </tr>
            </table>
          </td>
        </tr>
      </table>
    </td>
  </tr>
</table><!--<![endif]--></div></td></tr></table><table class=3D"html_block =
block-32" width=3D100% border=3D0 cellpadding=3D0 cellspacing=3D0 role=3Dpr=
esentation style=3Dmso-table-lspace:0;mso-table-rspace:0;mso-hide:all;displ=
ay:none;max-height:0;overflow:hidden><tr><td class=3Dpad><div style=3D"font=
-family:&#39;Google Sans&#39;,Roboto,arial,sans-serif;text-align:center" al=
ign=3Dcenter><!--[if false]><!--><div style=3D"vertical-align: top; text-al=
ign: start; padding-left: 18px; padding-right: 18px; font-weight: 400; font=
-size: 14px; color: #3c4043; line-height: 20px; letter-spacing: 0.2px;">
  If you want to stop using Sign in with Google with
  <a style=3D"color: inherit; text-decoration: none; cursor: default;">
    ecosia.org</a>, go to your Google Account.
</div><!--<![endif]--></div></td></tr></table><table class=3D"html_block bl=
ock-33" width=3D100% border=3D0 cellpadding=3D0 cellspacing=3D0 role=3Dpres=
entation style=3Dmso-table-lspace:0;mso-table-rspace:0;mso-hide:all;display=
:none;max-height:0;overflow:hidden><tr><td class=3Dpad><div style=3D"font-f=
amily:&#39;Google Sans&#39;,Roboto,arial,sans-serif;text-align:center" alig=
n=3Dcenter><!--[if false]><!--><!--<![endif]--></div></td></tr></table></td=
></tr></tbody></table></td></tr></tbody></table><!--<![endif]--><table clas=
s=3D"row row-11" align=3Dcenter width=3D100% border=3D0 cellpadding=3D0 cel=
lspacing=3D0 role=3Dpresentation style=3Dmso-table-lspace:0;mso-table-rspac=
e:0><tbody><tr><td><table class=3D"row-content stack" align=3Dcenter border=
=3D0 cellpadding=3D0 cellspacing=3D0 role=3Dpresentation style=3D"mso-table=
-lspace:0;mso-table-rspace:0;border-left:1px solid #e8eaed;border-radius:0;=
border-right:1px solid #e8eaed;color:#000;width:610px;margin:0 auto" width=
=3D610><tbody><tr><td class=3D"column column-1" width=3D100% style=3Dmso-ta=
ble-lspace:0;mso-table-rspace:0;font-weight:400;text-align:left;padding-bot=
tom:16px;padding-left:40px;padding-right:40px;padding-top:16px;vertical-ali=
gn:top><table class=3D"html_block block-1" width=3D100% border=3D0 cellpadd=
ing=3D0 cellspacing=3D0 role=3Dpresentation style=3Dmso-table-lspace:0;mso-=
table-rspace:0><tr><td class=3Dpad><div style=3D"font-family:&#39;Google Sa=
ns&#39;,Roboto,arial,sans-serif;text-align:center" align=3Dcenter></div></t=
d></tr></table><table class=3D"button_block block-4" width=3D100% border=3D=
0 cellpadding=3D0 cellspacing=3D0 role=3Dpresentation style=3Dmso-table-lsp=
ace:0;mso-table-rspace:0><tr><td class=3Dpad style=3Dpadding-bottom:16px;pa=
dding-top:16px;text-align:center><div class=3Dalignment align=3Dcenter><!--=
[if mso]>
<v:roundrect xmlns:v=3D"urn:schemas-microsoft-com:vml" xmlns:w=3D"urn:schem=
as-microsoft-com:office:word" href=3D"https://accounts.google.com/AccountCh=
ooser?Email=3Dvioletprouses@gmail.com&continue=3Dhttps://myaccount.google.c=
om/connections/overview/AWW5nWQ6SBCwNiYqwbs0wSM9S1afUFiNMthk2TUvTXA8Af7lkxj=
vdxsEzBAQ0tLQEyNAPtzA9t8ws8I3iDuFskAYe-Ze?utm_source=3De_notification&utm_m=
edium=3Demail_notification" style=3D"height:48px;width:268px;v-text-anchor:=
middle;" arcsize=3D"125%" stroke=3D"false" fillcolor=3D"#0b57d0">
<w:anchorlock/>
<v:textbox inset=3D"0px,0px,0px,0px">
<center dir=3D"false" style=3D"color:#ffffff;font-family:sans-serif;font-si=
ze:16px">
<![endif]-->
<a class=3Dbutton href=3Dhttps://c.gle/AKMee0eG0defh_cINk3BjPU8P9NHwQ0fVsLB=
8LlZXVc5nwFi61c6fsXSZJUBa5QSkLihDfxb9LrxkodJj0XLjoOepku3WTfNHPjax6bIfP3wLro=
JRjbHQXbQem4Ocdh1kHb_K0CkY-X9978EK1kwJWrmO921fWjYAyIckkW8SwifRlYzC4VNt1OSzJ=
xKqei4FHGXh0QCCGVTun5yIiLpBM0Kcdrer8tqicIsKecHJ4IjvOwiLqZi4Xz9fxEwmQJLWwIKc=
LnCwtiU6ENncPV4dvD82qBf4Qft5qGGt_czpP40u7VhBnk3TwYjTCByBPpJ45jLqEy00VSFwFBh=
0b_cFcjtmvWO1ywBYXYJSr3cvvdgPOPy_mJuJIXh37lwyV6VfOqxembEeFpsPUf9yJaLTAACCVQ=
v8ReXArwLDbyunE1mUlcVcfTX-4CPIX7c80b1bTJzwoSVctzYw3pT4AIcUZWoSECVi11nWk2eA0=
UriTVnrYJ4jDsNo9wwI0jQhBSXe-_pyRsnmpGdYWid-U275Zrz9xxm8We9X7ue7rD7cOMJsi764=
f7W9vLVNNyR6UMgmksd-5jPV7hYwJ-j4bKPIYWpNsIfwSAt9qNkP8oBLFI10ssIs0EpsnVBpfqn=
dYJUquG5CdKoZgucyqOJLOu-1J_Yjx8fOXnIxWSGk-L_WuWB74E1hVDD8xy63Wpkypm4EbL0mnj=
6VFUPgd2zNRJI1LAdWwOE0A target=3D_blank style=3D"background-color:#0b57d0;b=
order-bottom:0px solid transparent;border-left:0px solid transparent;border=
-radius:60px;border-right:0px solid transparent;border-top:0px solid transp=
arent;color:#ffffff;display:inline-block;font-family:&#39;Google Sans&#39;,=
Roboto,arial,sans-serif;font-size:16px;font-weight:500;mso-border-alt:none;=
padding-bottom:12px;padding-top:12px;text-align:center;text-decoration:none=
;width:auto;word-break:keep-all;"><span style=3D"word-break: break-word; pa=
dding-left: 32px; padding-right: 32px; font-size: 16px; display: inline-blo=
ck; letter-spacing: normal;"><span style=3D"word-break: break-word; line-he=
ight: 24px;">Go to your Google Account</span></span></a>
<!--[if mso]></center></v:textbox></v:roundrect><![endif]--></div></td></tr=
></table><table class=3D"html_block block-5" width=3D100% border=3D0 cellpa=
dding=3D0 cellspacing=3D0 role=3Dpresentation style=3Dmso-table-lspace:0;ms=
o-table-rspace:0><tr><td class=3Dpad><div style=3D"font-family:&#39;Google =
Sans&#39;,Roboto,arial,sans-serif;text-align:center" align=3Dcenter></div><=
/td></tr></table></td></tr></tbody></table></td></tr></tbody></table><table=
 class=3D"row row-12" align=3Dcenter width=3D100% border=3D0 cellpadding=3D=
0 cellspacing=3D0 role=3Dpresentation style=3Dmso-table-lspace:0;mso-table-=
rspace:0><tbody><tr><td><table class=3D"row-content stack" align=3Dcenter b=
order=3D0 cellpadding=3D0 cellspacing=3D0 role=3Dpresentation style=3D"mso-=
table-lspace:0;mso-table-rspace:0;border-left:1px solid #e8eaed;border-radi=
us:0;border-right:1px solid #e8eaed;color:#000;width:610px;margin:0 auto" w=
idth=3D610><tbody><tr><td class=3D"column column-1" width=3D100% style=3Dms=
o-table-lspace:0;mso-table-rspace:0;font-weight:400;text-align:left;padding=
-bottom:16px;padding-left:40px;padding-right:40px;vertical-align:top><table=
 class=3D"html_block block-1" width=3D100% border=3D0 cellpadding=3D0 cells=
pacing=3D0 role=3Dpresentation style=3Dmso-table-lspace:0;mso-table-rspace:=
0><tr><td class=3Dpad><div style=3D"font-family:&#39;Google Sans&#39;,Robot=
o,arial,sans-serif;text-align:center" align=3Dcenter><div style=3D"vertical=
-align: top; text-align: start; font-weight: 400; font-size: 14px; color: #=
3c4043; line-height: 20px; letter-spacing: 0.2px;">
  Review
  <a style=3D"color: inherit; text-decoration: none; cursor: default;">ecos=
ia.org</a>=E2=80=99s
  Privacy Policy and Terms of Service to understand how
  <a style=3D"color: inherit; text-decoration: none; cursor: default;">ecos=
ia.org</a>
  will process and protect your data.
</div></div></td></tr></table></td></tr></tbody></table></td>
</tr></tbody></table><table class=3D"row row-13" align=3Dcenter width=3D100=
% border=3D0 cellpadding=3D0 cellspacing=3D0 role=3Dpresentation style=3Dms=
o-table-lspace:0;mso-table-rspace:0><tbody><tr><td><table class=3D"row-cont=
ent stack" align=3Dcenter border=3D0 cellpadding=3D0 cellspacing=3D0 role=
=3Dpresentation style=3D"mso-table-lspace:0;mso-table-rspace:0;border-left:=
1px solid #e8eaed;border-radius:0;border-right:1px solid #e8eaed;color:#000=
;width:610px;margin:0 auto" width=3D610><tbody><tr><td class=3D"column colu=
mn-1" width=3D100% style=3Dmso-table-lspace:0;mso-table-rspace:0;font-weigh=
t:400;text-align:left;padding-bottom:16px;padding-left:40px;padding-right:4=
0px;vertical-align:top><table class=3D"html_block block-1" width=3D100% bor=
der=3D0 cellpadding=3D0 cellspacing=3D0 role=3Dpresentation style=3Dmso-tab=
le-lspace:0;mso-table-rspace:0><tr><td class=3Dpad><div style=3D"font-famil=
y:&#39;Google Sans&#39;,Roboto,arial,sans-serif;text-align:center" align=3D=
center><div style=3D"vertical-align: top; text-align: start; font-weight: 4=
00; font-size: 14px; color: #3c4043; line-height: 20px; letter-spacing: 0.2=
px;">
  If you want to delete the data you shared with
  <a style=3D"color: inherit; text-decoration: none; cursor: default;">ecos=
ia.org</a>,
  visit
  <a style=3D"color: inherit; text-decoration: none; cursor: default;">ecos=
ia.org</a>.
</div></div></td></tr>
</table></td></tr></tbody></table></td></tr></tbody></table><table class=3D=
"row row-14 mobile_hide" align=3Dcenter width=3D100% border=3D0 cellpadding=
=3D0 cellspacing=3D0 role=3Dpresentation style=3Dmso-table-lspace:0;mso-tab=
le-rspace:0><tbody><tr><td><table class=3D"row-content stack" align=3Dcente=
r border=3D0 cellpadding=3D0 cellspacing=3D0 role=3Dpresentation style=3D"m=
so-table-lspace:0;mso-table-rspace:0;border-left:1px solid #e8eaed;border-r=
adius:0;border-right:1px solid #e8eaed;color:#000;width:610px;margin:0 auto=
" width=3D610><tbody><tr><td class=3D"column column-1" width=3D100% style=
=3Dmso-table-lspace:0;mso-table-rspace:0;font-weight:400;text-align:left;pa=
dding-bottom:8px;vertical-align:top><table class=3D"html_block block-1" wid=
th=3D100% border=3D0 cellpadding=3D0 cellspacing=3D0 role=3Dpresentation st=
yle=3Dmso-table-lspace:0;mso-table-rspace:0><tr>
<td class=3Dpad><div style=3D"font-family:&#39;Google Sans&#39;,Roboto,aria=
l,sans-serif;text-align:center" align=3Dcenter><table cellspacing=3D0 cellp=
adding=3D0 border=3D0 width=3D100% style=3D"background-color: transparent;"=
>
  <tr>
    <td align=3Dcenter style=3D"padding: 0px 40px 8px;">
      <table cellspacing=3D0 cellpadding=3D0 border=3D0 width=3D100% style=
=3D"background-color: #transparent; border-radius: 12px; border: 1px solid =
#DADCE0;">
        <tr>
          <td style=3D"padding: 10px;">
            <table cellspacing=3D0 cellpadding=3D0 border=3D0 width=3D100%>
              <tr>
                <td style=3D"vertical-align: top; padding-left: 6px; paddin=
g-right: 6px;">
                  <p style=3D"margin: 2.4px;">
                    <img src=3Dhttps://www.gstatic.com/identity/boq/thirdpa=
rtyconnections/notification/20_x4.png height=3D24>
                  </p>
                </td>
                <td>
                  <table cellspacing=3D0 cellpadding=3D0 border=3D0 width=
=3D100%>
                    <tr>
                      <td style=3D"vertical-align: top; padding-bottom: 6px=
; padding-left: 6px; padding-right: 6px; color: #1F1F1F; font-size: 14px; l=
ine-height: 20px;">
                        <span style=3Dfont-weight:500;>
                          Safer with Google
                        </span>
                      </td>
                    </tr>
                    <tr>
                      <td style=3D"vertical-align: top; padding-left: 6px; =
padding-right: 6px; color: #444746; font-size: 12px; font-weight: 400; line=
-height: 16px; letter-spacing: 0.1px;">
                        Your Google Account protects your privacy with adva=
nced security designed to keep your data safe
                      </td>
                    </tr>
                  </table>
                </td>
              </tr>
            </table>
          </td>
        </tr>
      </table>
    </td>
  </tr>
</table></div></td></tr></table></td></tr></tbody></table></td></tr></tbody=
></table><!--[if !mso]><!--><table class=3D"row row-15 desktop_hide" align=
=3Dcenter width=3D100% border=3D0 cellpadding=3D0 cellspacing=3D0 role=3Dpr=
esentation style=3Dmso-table-lspace:0;mso-table-rspace:0;mso-hide:all;displ=
ay:none;max-height:0;overflow:hidden><tbody><tr><td><table class=3D"row-con=
tent stack" align=3Dcenter border=3D0 cellpadding=3D0 cellspacing=3D0 role=
=3Dpresentation style=3D"mso-table-lspace:0;mso-table-rspace:0;mso-hide:all=
;display:none;max-height:0;overflow:hidden;border-left:1px solid #e8eaed;bo=
rder-radius:0;border-right:1px solid #e8eaed;color:#000;width:610px;margin:=
0 auto" width=3D610><tbody><tr><td class=3D"column column-1" width=3D100% s=
tyle=3Dmso-table-lspace:0;mso-table-rspace:0;font-weight:400;text-align:lef=
t;padding-bottom:8px;vertical-align:top>
<table class=3D"html_block block-1" width=3D100% border=3D0 cellpadding=3D0=
 cellspacing=3D0 role=3Dpresentation style=3Dmso-table-lspace:0;mso-table-r=
space:0;mso-hide:all;display:none;max-height:0;overflow:hidden><tr><td clas=
s=3Dpad><div style=3D"font-family:&#39;Google Sans&#39;,Roboto,arial,sans-s=
erif;text-align:center" align=3Dcenter><!--[if false]><!--><table cellspaci=
ng=3D0 cellpadding=3D0 border=3D0 width=3D100% style=3D"background-color: t=
ransparent;">
  <tr>
    <td align=3Dcenter style=3D"padding: 0px 18px 8px;">
      <table cellspacing=3D0 cellpadding=3D0 border=3D0 width=3D100% style=
=3D"background-color: transparent; border-radius: 12px; border: 1px solid #=
DADCE0;">
        <tr>
          <td style=3D"padding: 10px;">
            <table cellspacing=3D0 cellpadding=3D0 border=3D0 width=3D100%>
              <tr>
                <td style=3D"vertical-align: top; padding-left: 6px; paddin=
g-right: 6px;">
                  <p style=3D"margin: 2.4px;">
                    <img src=3Dhttps://www.gstatic.com/identity/boq/thirdpa=
rtyconnections/notification/20_x4.png height=3D24>
                  </p>
                </td>
                <td>
                  <table cellspacing=3D0 cellpadding=3D0 border=3D0 width=
=3D100%>
                    <tr>
                      <td style=3D"vertical-align: top; padding-bottom: 6px=
; padding-left: 6px; padding-right: 6px; color: #1F1F1F; font-size: 14px; l=
ine-height: 20px;">
                        <span style=3Dfont-weight:600;>
                          Safer with Google
                        </span>
                      </td>
                    </tr>
                    <tr>
                      <td style=3D"vertical-align: top; padding-left: 6px; =
padding-right: 6px; color: #444746; font-size: 12px; font-weight: 400; line=
-height: 16px; letter-spacing: 0.1px;">
                        Your Google Account protects your privacy with adva=
nced security designed to keep your data safe
                      </td>
                    </tr>
                  </table>
                </td>
              </tr>
            </table>
          </td>
        </tr>
      </table>
    </td>
  </tr>
</table><!--<![endif]--></div></td></tr></table></td></tr></tbody></table><=
/td></tr></tbody></table><!--<![endif]--><table class=3D"row row-16" align=
=3Dcenter width=3D100% border=3D0 cellpadding=3D0 cellspacing=3D0 role=3Dpr=
esentation style=3Dmso-table-lspace:0;mso-table-rspace:0><tbody><tr><td><ta=
ble class=3D"row-content stack" align=3Dcenter border=3D0 cellpadding=3D0 c=
ellspacing=3D0 role=3Dpresentation style=3D"mso-table-lspace:0;mso-table-rs=
pace:0;border-left:1px solid #e8eaed;border-radius:0;border-right:1px solid=
 #e8eaed;color:#000;width:610px;margin:0 auto" width=3D610><tbody><tr><td c=
lass=3D"column column-1" width=3D100% style=3Dmso-table-lspace:0;mso-table-=
rspace:0;font-weight:400;text-align:left;padding-left:40px;padding-right:40=
px;vertical-align:top><table class=3D"html_block block-1" width=3D100% bord=
er=3D0 cellpadding=3D0 cellspacing=3D0 role=3Dpresentation style=3Dmso-tabl=
e-lspace:0;mso-table-rspace:0><tr><td class=3Dpad><div style=3D"font-family=
:&#39;Google Sans&#39;,Roboto,arial,sans-serif;text-align:center" align=3Dc=
enter></div></td></tr></table></td></tr></tbody></table></td></tr></tbody><=
/table><table class=3D"row row-19" align=3Dcenter width=3D100% border=3D0 c=
ellpadding=3D0 cellspacing=3D0 role=3Dpresentation style=3Dmso-table-lspace=
:0;mso-table-rspace:0><tbody><tr><td><table class=3D"row-content stack" ali=
gn=3Dcenter border=3D0 cellpadding=3D0 cellspacing=3D0 role=3Dpresentation =
style=3D"mso-table-lspace:0;mso-table-rspace:0;border-left:1px solid #e8eae=
d;border-right:1px solid #e8eaed;color:#000;border-bottom:1px solid #e8eaed=
;border-radius:0 0 8px 8px;width:610px;margin:0 auto" width=3D610><tbody><t=
r><td class=3D"column column-1" width=3D100% style=3Dmso-table-lspace:0;mso=
-table-rspace:0;font-weight:400;text-align:left;vertical-align:top><div cla=
ss=3D"spacer_block block-1" style=3Dheight:24px;line-height:24px;font-size:=
1px>=E2=80=8A</div></td></tr></tbody></table></td></tr>
</tbody></table><table class=3D"row row-20" align=3Dcenter width=3D100% bor=
der=3D0 cellpadding=3D0 cellspacing=3D0 role=3Dpresentation style=3Dmso-tab=
le-lspace:0;mso-table-rspace:0><tbody><tr><td><table class=3D"row-content s=
tack" align=3Dcenter border=3D0 cellpadding=3D0 cellspacing=3D0 role=3Dpres=
entation style=3D"mso-table-lspace:0;mso-table-rspace:0;border-radius:0;col=
or:#000;width:610px;margin:0 auto" width=3D610><tbody><tr><td class=3D"colu=
mn column-1" width=3D100% style=3Dmso-table-lspace:0;mso-table-rspace:0;fon=
t-weight:400;text-align:left;padding-left:27px;padding-right:27px;padding-t=
op:16px;vertical-align:top><table class=3D"paragraph_block block-1" width=
=3D100% border=3D0 cellpadding=3D0 cellspacing=3D0 role=3Dpresentation styl=
e=3Dmso-table-lspace:0;mso-table-rspace:0;word-break:break-word><tr><td cla=
ss=3Dpad style=3Dpadding-top:8px><div style=3Dcolor:#5f6368;direction:ltr;f=
ont-family:Roboto,Tahoma,Verdana,Segoe,sans-serif;font-size:10px;font-weigh=
t:400;letter-spacing:0;line-height:1.8;text-align:center;mso-line-height-al=
t:18px><p style=3Dmargin:0>You received this email to let you know about im=
portant changes to your Google Account and services.</p></div></td></tr></t=
able><table class=3D"paragraph_block block-2" width=3D100% border=3D0 cellp=
adding=3D0 cellspacing=3D0 role=3Dpresentation style=3Dmso-table-lspace:0;m=
so-table-rspace:0;word-break:break-word><tr><td class=3Dpad style=3Dpadding=
-top:8px><div style=3Dcolor:#5f6368;direction:ltr;font-family:Roboto,Tahoma=
,Verdana,Segoe,sans-serif;font-size:10px;font-weight:400;letter-spacing:0;l=
ine-height:1.2;text-align:center;mso-line-height-alt:12px><p style=3Dmargin=
:0;margin-bottom:0>
<span class=3DtinyMce-placeholder style=3D"word-break: break-word;">If you =
want to stop receiving these emails, you can <a href=3Dhttps://myaccount.go=
ogle.com/communication-preferences/unsubscribe/gt/AKMee0cW2nAB43XYf6HWrwG9G=
AUL5tEAgmZAM-HVy-WDpg33r6HZaoX9QJvIMhYkabviGgbxnCUyCSDOQxIz3qYJxJKvosGIJ4Tv=
j9opR2cMHZaap2_y4AtBZJc0QKLEFDcjscBI7BpOEVBp1ikfyjDPVgUdfHPuRZdeam_oL7SUo-9=
3SZ6XExqZzSCm2OnMjpE8tjS4BQYYTazxq8e_-AzOLFhQbqwEVlGZHGWgSn9jjet7j1Xgy63uS2=
e_oJcrohpHtuC1yGtV_FFtS2if3DybeZmQgn1ErBkqVo0ZMO9kRyTT?utm_source=3Dgm&amp;=
utm_medium=3Demail&amp;auto=3Dtrue target=3D_blank style=3D"text-decoration=
: none; color: #3b78e7;" rel=3Dnoopener>unsubscribe</a>.</span></p><p style=
=3Dmargin:0><span class=3DtinyMce-placeholder style=3D"word-break: break-wo=
rd;">Even if you unsubscribe from these emails, you=E2=80=99ll continue to =
receive security alerts.</span></p></div></td></tr></table><table class=3D"=
paragraph_block block-3" width=3D100% border=3D0 cellpadding=3D0 cellspacin=
g=3D0 role=3Dpresentation style=3Dmso-table-lspace:0;mso-table-rspace:0;wor=
d-break:break-word><tr><td class=3Dpad style=3Dpadding-top:8px><div style=
=3Dcolor:#5f6368;direction:ltr;font-family:Roboto,Tahoma,Verdana,Segoe,sans=
-serif;font-size:10px;font-weight:400;letter-spacing:0;line-height:1.8;text=
-align:center;mso-line-height-alt:18px><p style=3Dmargin:0>=C2=A9 2026 Goog=
le LLC 1600 Amphitheatre Parkway, Mountain View, CA 94043=C2=A0</p></div></=
td></tr></table></td></tr></tbody></table></td></tr></tbody></table></td></=
tr></tbody></table><!-- End -->
</body></html>
--00000000000015913906592459b2--

From 1873662015199482354@xxx Sun Aug 16 06:55:41 +0000 2026
X-GM-THRID: 1873662015199482354
X-Gmail-Labels: Inbox,Category Personal,Unread
Delivered-To: violetprouses@gmail.com
Received: by 2002:a17:504:b30a:20b0:1e7e:8814:2405 with SMTP id e10-n2csp1487645njt;
        Sat, 15 Aug 2026 23:55:41 -0700 (PDT)
X-Received: by 2002:a05:6820:83cc:10b0:6a1:7790:258e with SMTP id 006d021491bc7-6b0d6257e08mr11655760eaf.18.1786863341136;
        Sat, 15 Aug 2026 23:55:41 -0700 (PDT)
ARC-Seal: i=1; a=rsa-sha256; t=1786863341; cv=none;
        d=google.com; s=arc-20260327;
        b=BLk9sfpcldYZUvfCRK6lbd4TjYDQkGDgVLjsswyZNTxPXJpFowI8wFLNRzo9I/SP1R
         o+3ijCYS5fUE2HbsykEuqxmb8WKoo5KCLO0GgOgd8LAV6d9wy+F6FH2IAW2Bu4/Pxl4g
         k047//bMmDZn3v7DNqwOWeWBiFQg8YiXsCRqRyQyzY9lrL7BM5jp8/Ne3sY9BDeYDCIM
         qMIpr2Ex9Zr2geRlm8go/RDNKbLz8rF+9yWU2qaceHI4mpddLFvWr2Jl9BZF8B1Az5Xg
         o5CZBzdLr7ZUyEDPMrzZE4OCuimyNx+qMiBDWpm+PpMVEde8jh2O0UUhKYmqApKqowCO
         55sw==
ARC-Message-Signature: i=1; a=rsa-sha256; c=relaxed/relaxed; d=google.com; s=arc-20260327;
        h=to:from:subject:message-id:gmsai:date:mime-version:dkim-signature;
        bh=tRVbmCLUEc0n1Bdww5AyklBfW+iE2oe5S01+YQtqafE=;
        fh=hUfB+x8fKgVbMvTJ7mEk0I28xQ+Z9a/Un/iVPLaMuVQ=;
        b=Pl4egoXK/gPKkG1bnqZhDqG9acsQCXKrQrfF1TXPgTAc7e0AU99haapagsqkjfWZMP
         uCLLPlk0YsbzTJLDLrR8uYaeleJmIdLMfFXy5BEIg3I22P/GSKiLwHuhSm1mpeUt9n1t
         YHW7nzS+5YpGs4oKIpLPheD5GR9y1HQk/QckX1rh3gaztHtjEbU1f2Cjg8OtJMV/RomL
         Y1AAaEykWJPjQErs9w4Z0EUxzacutTeyYW3M/95AQRywQPczohG84K1VWU28G/wG6Zmv
         RqrjoLTUiF2X5rsJcYOOXEAtYbHc3jqUudRDdMR9+kIOP93HB6MMsAORcFXgiQbIgrcc
         w4LA==;
        dara=google.com
ARC-Authentication-Results: i=1; mx.google.com;
       dkim=pass header.i=@google.com header.s=20251104 header.b=ZuyBzJtw;
       spf=pass (google.com: domain of 37f6bahakdqsqlxtwtp3-yz2p0w9rzzrwp.nzx6tzwp402z53p3rxltw.nzx@chime-notifications.bounces.google.com designates 209.85.220.69 as permitted sender) smtp.mailfrom=37F6BahAKDQsqlxtwtp3-yz2p0w9rzzrwp.nzx6tzwp402z53p3rxltw.nzx@chime-notifications.bounces.google.com;
       dmarc=pass (p=REJECT sp=REJECT dis=NONE) header.from=google.com;
       dara=pass header.i=@gmail.com
Return-Path: <37F6BahAKDQsqlxtwtp3-yz2p0w9rzzrwp.nzx6tzwp402z53p3rxltw.nzx@chime-notifications.bounces.google.com>
Received: from mail-sor-f69.google.com (mail-sor-f69.google.com. [209.85.220.69])
        by mx.google.com with SMTPS id 586e51a60fabf-45e8f9b284esor2752404fac.4.2026.08.15.23.55.41
        for <violetprouses@gmail.com>
        (Google Transport Security);
        Sat, 15 Aug 2026 23:55:41 -0700 (PDT)
Received-SPF: pass (google.com: domain of 37f6bahakdqsqlxtwtp3-yz2p0w9rzzrwp.nzx6tzwp402z53p3rxltw.nzx@chime-notifications.bounces.google.com designates 209.85.220.69 as permitted sender) client-ip=209.85.220.69;
Authentication-Results: mx.google.com;
       dkim=pass header.i=@google.com header.s=20251104 header.b=ZuyBzJtw;
       spf=pass (google.com: domain of 37f6bahakdqsqlxtwtp3-yz2p0w9rzzrwp.nzx6tzwp402z53p3rxltw.nzx@chime-notifications.bounces.google.com designates 209.85.220.69 as permitted sender) smtp.mailfrom=37F6BahAKDQsqlxtwtp3-yz2p0w9rzzrwp.nzx6tzwp402z53p3rxltw.nzx@chime-notifications.bounces.google.com;
       dmarc=pass (p=REJECT sp=REJECT dis=NONE) header.from=google.com;
       dara=pass header.i=@gmail.com
DKIM-Signature: v=1; a=rsa-sha256; c=relaxed/relaxed;
        d=google.com; s=20251104; t=1786863341; x=1787468141; dara=google.com;
        h=content-type:to:from:subject:message-id:gmsai:date:mime-version
         :from:to:cc:subject:date:message-id:reply-to:content-type;
        bh=tRVbmCLUEc0n1Bdww5AyklBfW+iE2oe5S01+YQtqafE=;
        b=ZuyBzJtwPqPLgn9ARBPK4dSCbDpD/TXuWgl225L6uM8vKp4dio5RooW7dmrF1Ea7Jv
         esT1OEFp5K8A5rT5SgXJmXdAdCsDAmuUZcvIfXjnHnTZHy8IeHRJWpemOiB672xnTotE
         keOGCJ076ob586KLooKKNwoHg2h8yByH+V1xNC2/BQAgQ7UjRcAvjG533oExjmQ5HdF+
         OoEFhw4INCobYieDR+DnD5EZIVsTEtt32Qf5TG3wQSldeXaccTf50QnklvIgGLT3zz0k
         1ewyOfbUb8TOejJk9wAFFnrVAnat3NUbdz1d/4HWOFYpTMMiOwJRNFNKpD9EhX3y57Sk
         DJTQ==
X-Google-DKIM-Signature: v=1; a=rsa-sha256; c=relaxed/relaxed;
        d=1e100.net; s=20251104; t=1786863341; x=1787468141;
        h=content-type:to:from:subject:message-id:gmsai:date:mime-version
         :x-gm-message-state:from:to:cc:subject:date:message-id:reply-to
         :content-type;
        bh=tRVbmCLUEc0n1Bdww5AyklBfW+iE2oe5S01+YQtqafE=;
        b=PAAUOOXZTB1xCSi417yPcmwSkQXwyS3Wgyu3mlPYsRNNzIVwrvljk6xC8PZQDWJavP
         4JESTag8EkaUq1Z2iUcIOejUotEbMFnRg85wPe7zRgl4HkyR4+0zvTqPoKZAjoiItfvD
         FEAMoDXI0ab+TP6dkap3KUnHD1ep8nQjwZHB7FqL70t14b9JjdYtf+SgoAOCCrSQUwiq
         cfxxotURpjLv4JfOwrf6P2f6L2jdDrrepDfbuIMzOYwsGYFs+oiWw1x9C0bP2RX1lkGI
         /x5bBp4hkcosw4EE4CmFIEQzmXQj6bq3pPmyFB9aaSYzNn7tPQOMi2eQ8rQyRI7yk8K4
         M7hA==
X-Gm-Message-State: AOJu0Yw9OuqPjiRS4wvX3hfNfG9elQ+XK7bp9ZJbjmg+9SOT0suLwhoL
	qGermk21o3L+09XbgQf4VOR3Z1cW4CuJ7+iyqahf4T8PeynQmS11F9gDTdOqlQ3vU0MmiwvhK4A
	1iea5iNBqTGbitJQDPc7nZn2K
MIME-Version: 1.0
X-Received: by 2002:a05:6808:179d:b0:489:a387:1e29 with SMTP id
 5614622812f47-4b241f24686mr14385043b6e.20.1786863340873; Sat, 15 Aug 2026
 23:55:40 -0700 (PDT)
Date: Sat, 15 Aug 2026 23:55:40 -0700
gmsai: true
X-Google-Notification-Metadata: CgISAA
X-Notifications: a0986a75b0d803f8
X-Notifications-Bounce-Info: AWKoMQRaFU3KTc2B_ilzKlj-fx99YJt3IStCm0kN7HZaFmK-B5awHasERHK6nwytLoFsHI5FXVWiLt_A-nEmHNL32tlOXs7vYke9n29qNDuESg8Ft_j2xXPQODimn1NR4-rUpZmMYrwPvUcyJ9f59GZJJ90bmju8Dy6Qo36ZRmHBkb3jxmrrOW82CtCrLkRroyqmPcPXjPvZkd0iUdLbBk_0io3ISw3u1aCjJBiCNjAwNjA0MDQxNTM1NTk2OTMzMg
Message-ID: <RHu9ybbC9kzuPzLVpJ5w2g@notifications.google.com>
Subject: An issue with your family group
From: Google  <families-noreply@google.com>
To: violetprouses@gmail.com
Content-Type: multipart/alternative; boundary="000000000000b1f2420659248a60"

--000000000000b1f2420659248a60
Content-Type: text/plain; charset="UTF-8"; format=flowed; delsp=yes
Content-Transfer-Encoding: base64

DQpZb3VyIGZhbWlseSBncm91cCBpcyB1bmF2YWlsYWJsZSByaWdodCBub3cNCg0KSXQgbG9va3Mg
bGlrZSB0aGVyZeKAmXMgYSBwcm9ibGVtIHdpdGggeW91ciBmYW1pbHkgZ3JvdXAuIEl0IG1heSB0
YWtlIHNvbWUgIA0KdGltZSBiZWZvcmUgeW91IGNhbiB1c2UgaXQgYWdhaW4uDQoNCkZvciBub3cs
IHlvdSBjYW4gbm8gbG9uZ2VyIGFjY2VzcyBHb29nbGUgcHJvZHVjdHMgYW5kIHNlcnZpY2VzIHRo
YXQgbmVlZCBhICANCmZhbWlseSBncm91cCB0byB3b3JrLiBMZWFybiBtb3JlICANCjxodHRwczov
L3N1cHBvcnQuZ29vZ2xlLmNvbS9nb29nbGVwbGF5P3A9ZW1haWxfZmFtaWx5ZGlzYWJsZWQ+DQoN
CiAgICAtDQoNCiAgICBJZiB5b3VyIGZhbWlseSBtYW5hZ2VyIHB1cmNoYXNlZCBhbnkgZmFtaWx5
IHN1YnNjcmlwdGlvbiwgeW91IGNhbiBrZWVwICANCnVzaW5nIGl0IHVudGlsIHRoZSBuZXh0IGJp
bGxpbmcgY3ljbGUgc3RhcnRzLg0KDQpJdCdzIGEgZ29vZCBpZGVhIHRvIGFzayB0aGUgZmFtaWx5
IG1hbmFnZXIgYWJvdXQgdGhpcyBlbWFpbC4gSWYgeW91IHdhbnQgdG8gIA0KY3JlYXRlIG9yIGpv
aW4gYSBuZXcgZmFtaWx5IGdyb3VwLCB5b3UgY2FuIGxlYXZlIHRoaXMgZmFtaWx5IGdyb3VwIGF0
IGFueSAgDQp0aW1lLg0KTGVhdmUgZmFtaWx5IGdyb3VwIDxodHRwczovL215YWNjb3VudC5nb29n
bGUuY29tL2ZhbWlseS9sZWF2ZT4NCg0KWW91IHJlY2VpdmVkIHRoaXMgbWFuZGF0b3J5IGVtYWls
IHNlcnZpY2UgYW5ub3VuY2VtZW50IHRvIHVwZGF0ZSB5b3UgYWJvdXQgIA0KaW1wb3J0YW50IGNo
YW5nZXMgdG8geW91ciBHb29nbGUgcHJvZHVjdCBvciBhY2NvdW50LsKpMjAyNiBHb29nbGUgTExD
LCAxNjAwICANCkFtcGhpdGhlYXRyZSBQYXJrd2F5LCBNb3VudGFpbiBWaWV3LCBDQSA5NDA0Mywg
VVNBDQoNCg0K
--000000000000b1f2420659248a60
Content-Type: text/html; charset="UTF-8"
Content-Transfer-Encoding: quoted-printable

<body style=3D"background: #fff; font: 400 24px Google Sans; margin: auto; =
max-width: 600px; min-width: 348px; padding: 0 0;"><div style=3D"background=
: #fff; box-sizing: border-box; margin: auto; max-width: 500px;border: 1px =
solid #e8eaed; padding: 32px 16px; border-radius: 8px;"><div style=3D"paddi=
ng:0 0  10px ;"><img style=3D"display: block; height: 32px; margin:auto; pa=
dding: 0 0;" src=3D"https://ssl.gstatic.com/images/branding/googlelogo/2x/g=
ooglelogo_color_120x44dp.png" alt=3D""/></div><h1 style=3D"margin: 0; text-=
align: center; font: 400 24px 'Google Sans',Roboto,Helvetica,Arial,sans-ser=
if;color: #202124; line-height: 32px; padding: 0 0 10px;">Your family group=
 is unavailable right now</h1><div style=3D"border: 1px solid #dadce0; marg=
in: 24px 0"></div><p style=3D"color:#202124; max-width: 456px; letter-spaci=
ng: 0.2px; font: 400 14px &#39;Google Sans&#39;,Roboto,Helvetica,Arial,sans=
-serif;line-height: 20px; margin: 24px 0;">It looks like there=E2=80=99s a =
problem with your family group. It may take some time before you can use it=
 again.</p><p style=3D"color:#202124; max-width: 456px; letter-spacing: 0.2=
px; font: 400 14px &#39;Google Sans&#39;,Roboto,Helvetica,Arial,sans-serif;=
line-height: 20px; margin: 24px 0;">For now, you can no longer access Googl=
e products and services that need a family group to work. <a href=3D"https:=
//support.google.com/googleplay?p=3Demail_familydisabled" style=3D"color: #=
458af4;">Learn more</a></p><ul><li><p style=3D"color:#202124; font: 400 14p=
x 'Google Sans',Roboto,Helvetica,Arial,sans-serif; line-height: 20px; margi=
n: 10px 0; max-width:456px; letter-spacing:0.2px;">If your family manager p=
urchased any family subscription, you can keep using it until the next bill=
ing cycle starts.</p></li></ul><p style=3D"color:#202124; max-width: 456px;=
 letter-spacing: 0.2px; font: 400 14px &#39;Google Sans&#39;,Roboto,Helveti=
ca,Arial,sans-serif;line-height: 20px; margin: 24px 0;">It's a good idea to=
 ask the family manager about this email. If you want to create or join a n=
ew family group, you can leave this family group at any time.</p><div style=
=3D"margin: 0 auto; max-width:456px; text-align:center;"><a style=3D"color:=
 #fff; letter-spacing: 0.25px; display: inline-block; text-align: center; t=
ext-decoration:none; font: 500 14px 'Google Sans',Roboto,Helvetica,Arial,sa=
ns-serif;padding: 8px 24px; background: #1a73e8; border-radius: 4px; line-h=
eight: 20px;" href=3D"https://myaccount.google.com/family/leave" link-id=3D=
"family-deactivated-leave-family-group">Leave family group</a></div></div><=
footer style=3D"max-width: 499px; color: #888; margin: auto; font: 400 11px=
 'Google Sans',Roboto,Helvetica,Arial,sans-serif;letter-spacing: 0.2px;"><p=
>You received this mandatory email service announcement to update you about=
 important changes to your Google product or account.<span>&copy;2026 Googl=
e LLC, 1600 Amphitheatre Parkway, Mountain View, CA 94043, USA</span></p></=
footer></body>
--000000000000b1f2420659248a60--
