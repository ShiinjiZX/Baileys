# <div align='center'>Baileys - Typescript/Javascript WhatsApp Web API</div>

<div align="center"><img src="https://freeimage.host/i/3FKUya2"></div>

## Catatan Penting

Repository Asli: [WhiskeySockets](https://github.com/WhiskeySockets). Sebuah Baileys yang sudah ditingkatkan dengan menambah beberapa fitur yang tidak ada dalam Repository Aslinya.

## Install

Instal di package.json:
```json
"dependencies": {
    "@whiskeySockets/baileys": "github:ShiinjiZX/Baileys",
	"jimp": "latest"
}
```
atau install menggunakan terminal:
```
npm install @whiskeySockets/baileys@github:ShiinjiZX/Baileys

npm install jimp@latest
```

Masukan ke dalam kode project mu:
```ts 
// type esm
import makeWASocket from '@whiskeySockets/baileys'
```

```js
// type cjs
const { default: makeWASocket } = require("@whiskeySockets/baileys")
```

## Fitur Tambahan dan Perbaikan
Berikut adalah beberapa fitur dan peningkatan yang telah di tambahkan:

- **Dukungan untuk Mengirim Pesan ke Channel**: Kini Anda dapat mengirim pesan ke saluran dengan mudah.

- **Dukungan untuk Pesan Tombol dan Pesan Interaktif**: Menambahkan kemampuan untuk mengirim pesan dengan tombol dan pesan interaktif.

- **Ikon Pesan AI**: Menambahkan pengaturan ikon AI yang dapat disesuaikan untuk pesan

- **Pengaturan Gambar Profil**: Memungkinkan pengguna mengunggah gambar profil dalam ukuran aslinya tanpa pemotongan, memastikan kualitas dan tampilan visual yang lebih baik.

- **Kode Pasangan Kustom**: Kini pengguna dapat membuat dan menyesuaikan kode pasangan sesuai keinginan, meningkatkan kenyamanan dan keamanan saat menghubungkan perangkat.

- **Perbaikan Libsignal**: Membersihkan log untuk keluaran yang lebih bersih dan lebih informatif.

Lebih banyak fitur dan peningkatan akan ditambahkan di masa mendatang.

## Contoh Fitur

### NEWSLETTEXR

- **Untuk mendapatkan info newsletter**
``` ts
const metadata = await sock.newsletterMetadata("invite", "xxxxx")
// or
const metadata = await sock.newsletterMetadata("jid", "abcd@newsletter")
console.log(metadata)
```
- **Untuk memperbarui deskripsi newsletter**
``` ts
await sock.newsletterUpdateDescription("abcd@newsletter", "New Description")
```
- **Untuk memperbarui nama suatu newsletter**
``` ts
await sock.newsletterUpdateName("abcd@newsletter", "New Name")
```  
- **Untuk memperbarui gambar profil newsletter**
``` ts
await sock.newsletterUpdatePicture("abcd@newsletter", buffer)
```
- **Untuk menghapus gambar profil newsletter**
``` ts
await sock.newsletterRemovePicture("abcd@newsletter")
```
- **Untuk menonaktifkan notifikasi newsletter**
``` ts
await sock.newsletterUnmute("abcd@newsletter")
```
- **Untuk menonaktifkan notifikasi newsletter**
``` ts
await sock.newsletterMute("abcd@newsletter")
```
- **Untuk membuat newsletter**
``` ts
const metadata = await sock.newsletterCreate("Nama newsletter", "newsletter Deskripsi")
console.log(metadata)
```
- **Untuk menghapus newsletter**
``` ts
await sock.newsletterDelete("abcd@newsletter")
```
- **Untuk mengikuti newsletter**
``` ts
await sock.newsletterFollow("abcd@newsletter")
```
- **Untuk berhenti mengikuti newsletter**
``` ts
await sock.newsletterUnfollow("abcd@newsletter")
```
- **Untuk mengirim reaksi**
``` ts
// jid, id pesan & emotikon
// cara mendapatkan ID adalah dengan menyalin url pesan dari saluran
// Contoh: [ https://whatsapp.com/channel/xxxxx/175 ]
// Angka terakhir URL adalah ID
const id = "175"
await sock.newsletterReactMessage("abcd@newsletter", id, "🥳")
```

### BUTTON MESSAGE & INTERACTIVE MESSAGE

- **Untuk mengirim button dengan teks**
```ts
const buttons = [
  { buttonId: 'id1', buttonText: { displayText: 'Button 1' }, type: 1 },
  { buttonId: 'id2', buttonText: { displayText: 'Button 2' }, type: 1 }
]

const buttonMessage = {
    text: "Hi it's button message",
    footer: 'Hello World',
    buttons,
    headerType: 1,
    viewOnce: true
}

await sock.sendMessage(id, buttonMessage, { quoted: null })
```
- **Untuk mengirim button dengan gambar**
```ts
const buttons = [
  { buttonId: 'id1', buttonText: { displayText: 'Button 1' }, type: 1 },
  { buttonId: 'id2', buttonText: { displayText: 'Button 2' }, type: 1 }
]

const buttonMessage = {
    image: { url: "https://example.com/abcd.jpg" }, // image: buffer or path
    caption: "Hi it's button message with image",
    footer: 'Hello World',
    buttons,
    headerType: 1,
    viewOnce: true
}

await sock.sendMessage(id, buttonMessage, { quoted: null })

```
- **Untuk mengirim button dengan video**
```ts
const buttons = [
  { buttonId: 'id1', buttonText: { displayText: 'Button 1' }, type: 1 },
  { buttonId: 'id2', buttonText: { displayText: 'Button 2' }, type: 1 }
]

const buttonMessage = {
    video: { url: "https://example.com/abcd.mp4" }, // video: buffer or path
    caption: "Hi it's button message with video",
    footer: 'Hello World',
    buttons,
    headerType: 1,
    viewOnce: true
}

await sock.sendMessage(id, buttonMessage, { quoted: null })
```

- **Untuk mengirim pesan interaktif**
```ts
const interactiveButtons = [
     {
        name: "quick_reply",
        buttonParamsJson: JSON.stringify({
             display_text: "Quick Reply",
             id: "ID"
        })
     },
     {
        name: "cta_url",
        buttonParamsJson: JSON.stringify({
             display_text: "Tap Here!",
             url: "https://www.example.com/"
        })
     },
     {
        name: "cta_copy",
        buttonParamsJson: JSON.stringify({
             display_text: "Copy Code",
             id: "12345",
             copy_code: "12345"
        })
     }
]

const interactiveMessage = {
    text: "Hello World!",
    title: "this is the title",
    footer: "this is the footer",
    interactiveButtons
}

await sock.sendMessage(id, interactiveMessage, { quoted: null })
```
- **Untuk mengirim pesan interaktif dengan gambar**
```ts
const interactiveButtons = [
     {
        name: "quick_reply",
        buttonParamsJson: JSON.stringify({
             display_text: "Quick Reply",
             id: "ID"
        })
     },
     {
        name: "cta_url",
        buttonParamsJson: JSON.stringify({
             display_text: "Tap Here!",
             url: "https://www.example.com/"
        })
     },
     {
        name: "cta_copy",
        buttonParamsJson: JSON.stringify({
             display_text: "Copy Code",
             id: "12345",
             copy_code: "12345"
        })
     }
]

const interactiveMessage = {
    image: { url: "https://example.com/abcd.jpg" }, // image: buffer or path
    caption: "this is the caption",
    title: "this is the title",
    footer: "this is the footer",
    interactiveButtons
}

await sock.sendMessage(id, interactiveMessage, { quoted: null })
```
- **Untuk mengirim pesan interaktif dengan video**
```ts
const interactiveButtons = [
     {
        name: "quick_reply",
        buttonParamsJson: JSON.stringify({
             display_text: "Quick Reply",
             id: "ID"
        })
     },
     {
        name: "cta_url",
        buttonParamsJson: JSON.stringify({
             display_text: "Tap Here!",
             url: "https://www.example.com/"
        })
     },
     {
        name: "cta_copy",
        buttonParamsJson: JSON.stringify({
             display_text: "Copy Code",
             id: "12345",
             copy_code: "12345"
        })
     }
]

const interactiveMessage = {
    video: { url: "https://example.com/abcd.mp4" }, // video: buffer or path
    caption: "this is the caption",
    title: "this is the title",
    footer: "this is the footer",
    interactiveButtons
}

await sock.sendMessage(id, interactiveMessage, { quoted: null })
```

### AI Icon

```ts
// just add "ai: true" function to sendMessage
await sock.sendMessage(id, { text: "Hello Wold", ai: true })
```

### Custom Code Pairing

```ts
if(usePairingCode && !sock.authState.creds.registered) {
    const phoneNumber = await question('Please enter your mobile phone number:\n')
    const custom = "NSTRCODE" // must be 8 digits, can be letters or numbers
    const code = await sock.requestPairingCode(phoneNumber, custom)
    console.log(`Pairing code: ${code?.match(/.{1,4}/g)?.join('-') || code}`)
}
```

## Reporting Issues
Jika Anda mengalami masalah saat menggunakan repositori ini atau bagian mana pun darinya, jangan ragu untuk membuka[new issue](https://github.com/nstar-y/Bail/issues) Di Sini.

## Notes
Segala sesuatu selain modifikasi yang disebutkan di atas tetap sama dengan repositori asli. Anda dapat memeriksa repositori asli di [WhiskeySockets](https://github.com/WhiskeySockets/Baileys)