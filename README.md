#  Hoja de vida by Jesus Torres. Hecha en Vue 3

This theme offers a simple and clean design tailored for creating user-friendly website resumes or CV landing pages. It's built using Vue 3.0 (Composition API) and Bootstrap 5, presenting a cohesive one-page layout that blends functionality and aesthetics.

Key features:
- An anchored fixed side navigation bar for smooth scrolling through the page.
- Six custom section layouts showcasing work experience, educational background, professional skills, portfolio, and more.
- A tailored navigation mode specifically for mobile screens.
- Multi-language translation support included.
- Using Vite for faster build times and seamless integration.


## Demostraciòn


1. Navigate to the root directory of the project and install all dependencies with npm:
```
npm install
```

2. Run the project in developer mode:
```
npm run dev
```

3. To temporarily deactivate the preload animation during theme adjustments, navigate to `public/data/settings.json` and modify the following field:

```
 "preloaderEnabled": false
```

## Template Customization

### 1. Changing the content

The application content, including texts and images, is conveniently stored within the `public/` folder. Inside this directory, you'll come across two folders:

- `public/data` ➔ This directory hosts a collection of JSON files that house the entirety of the application's content.
- `public/images`➔ Here, you'll find a collection of icons and photos that the application utilizes.

You can personalize the app's content by modifying the data within these two folders according to your preferences. 


### 2. Adding and removing languages

To add or remove languages, open `public/data/settings.json` and modify the `supportedLanguages` field as needed. Use the `default` property to specify the fallback language that should be used if the application doesn't support the user's preferred language.

```json
{
    "supportedLanguages": [
        {
            "name": "English",
            "id": "en",
            "flagUrl": "images/flags/en.png",
            "default": true
        },

        {
            "name": "日本語",
            "id": "ja",
            "flagUrl": "images/flags/ja.png"
        }
    ]
}
```

The `public/images/flags/` folder already contains a collection of flags for commonly used languages. If you require a specific flag icon that isn't there, you can download it at no cost from this [source](https://www.flaticon.com/packs/countrys-flags).

To deactivate support for multiple languages, keep only a single language within the array. This will automatically hide the language picker menu.

### 3. Adding, removing and reordering sections

Inside the `public/data/sections.json` file, you will come across two arrays: one for sections and the other for categories. Every section in the application should be linked to a corresponding category. These categories are used in grouping sections within the mobile navigation.

Adding, removing or reordering the portfolio sections and categories can be achieved by making modifications to these arrays as needed.

For localizing the section and category titles, ensure that the `id` of each section and category has a corresponding translation in `public/data/strings.json`.

*public/data/strings.json*
```json 
{
    "en": {
        "section1_id": "Section 1 ID",
        "section2_id": "Section 2 ID",
        "section3_id": "Section 3 ID"
    },
    
    "ja": {
        "section1_id": "セクション1 ID",
        "section2_id": "セクション2 ID",
        "section3_id": "セクション3 ID"
    }
}
```

### 4. Customizing a section

Each section entry in `public/data/sections.json` comprises the following fields:

```json 
{
    "id": "experience",
    "categoryId": "background",
    "component": "TimelineSection",
    "jsonPath": "data/sections/experience.json",
    "faIcon": "fa-solid fa-briefcase"
}
```

- ***id*** ➔ A unique identifier for the section, also used as a key to fetch the section's name within `strings.json`
- ***categoryId*** ➔ Specifies the category to which the section belongs.
- ***component*** ➔ Indicates the Vue component responsible for rendering the section.
- ***jsonPath*** ➔ A reference pointing to the JSON file containing the section's content.
- ***faIcon*** ➔ The FontAwesome icon associated with the section.

To modify the content of a section, open and edit its respective JSON file. Keep in mind that each Vue component may require a specific JSON structure. For proper structuring of section JSON files, refer to the existing ones as a guide.

### 5. Adding functionality to the contact form

Making the contact form functional requires the creation of your own server-side implementation within the `ContactForm.vue` file. Please note that the current template only includes the client-side implementation, accompanied by a simulated delay using a placeholder timeout to mimic the waiting period for requests:


```js
const _sendMessage = (values) => {
    const feedbackView = layout.getFeedbackView()
    feedbackView.showActivitySpinner(data.getString("sendingMessage") + "...")
    submitAttempts++

}
```

## Building for production

Open the `vite.config.js` file and set the base directory for your application. This setting defines the main path that your website will be hosted under.

```js
export default defineConfig({
  base: '/resumecv',
  plugins: [vue()],
})