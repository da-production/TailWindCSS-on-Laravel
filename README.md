[<img src="https://miro.medium.com/max/450/1*9V4r2JpA02Jzu0Tro-i6hg.png">](http://google.com.au/)

# TailWindCSS-on-Laravel
In this short tutorial, I will go over on how you can install TailWindCSS on Laravel project.
Although you can install tailwind on any of your Laravel Project (old or new). For the demonstration purpose.

### Step 1:
Open Terminal / Command-line and navigate to the project root directory and run the following command.
```
npm install tailwindcss
```

### Step 2: Add TailWind to CSS
Now, we are ready to use tailwind css in your project. By default Laravel project comes installed with Bootstrap as a default front-end framework. Since we are going to use tailwind css we will remove the bootstrap imports and replace them with tailwindcss.

Open file app.scss which is located under folder resources > sass.

Remove the following import from the file 
```
// Fonts
@import url('https://fonts.googleapis.com/css?family=Nunito');

// Variables
@import 'variables';

// Bootstrap
@import '~bootstrap/scss/bootstrap';
```

```
@tailwind base;

@tailwind components;

@tailwind utilities;
```

### Step 3: Create your Tailwind config file 
Next up, we need to generate a tailwind config file, This fill will be used by laravel mix (webpack) while converting the scss file into css.

Run the following command to generate the config file.
```
npx tailwind init
```
This command will generate tailwind.config.js file in your project root directory.
```
// tailwind.config.js
module.exports = {
  theme: {},
  variants: {},
  plugins: [],
}
```

### Step 4: Include Tailwind in Laravel Mix Build Process 
Next up, we need to tell Laravel Mix (which internally uses webpack) to compile tailwind sass using the tailwind configuration file.

Open the webpack.mix.js file and make the following changes.
```
const mix = require('laravel-mix');

/*
 |--------------------------------------------------------------------------
 | Mix Asset Management
 |--------------------------------------------------------------------------
 |
 | Mix provides a clean, fluent API for defining some Webpack build steps
 | for your Laravel application. By default, we are compiling the Sass
 | file for the application as well as bundling up all the JS files.
 |
 */

mix.js('resources/js/app.js', 'public/js');
    
const tailwindcss = require('tailwindcss')

mix.sass('resources/sass/app.scss', 'public/css')
   .options({
      processCssUrls: false,
      postCss: [ tailwindcss('tailwind.config.js') ],
})
```
### Step 5:Run NPM
We are now ready to run the npm build process, run the following command in your terminal / command-line
```
npm run dev or npm run watch
```
This will compile you tailwindcss code and will put them into app.css file located in public / css directory.

That’s all about the installation.

:)
