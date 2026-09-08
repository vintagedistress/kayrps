## RP Character & Thread Tracker
This version of the RP Character and Thread Tracker has been designed to _not_ use a local compilation step, but only basic HTML, CSS, and JS. If you would like the version that uses SASS and Gulp-based HTML templating, please reach out on Discord (luxacious11) and I will happily package it for you into a ZIP file. However, keep in mind you will need: Node v12.22.12 (recommended to be installed with NVM for version management) and a Command Line Interface system that has permissions to run npm, yarn, and git commands.

### Before Setup
1. Ensure you have a [GitHub](https://github.com/) account create and a repository made to host the code. Personally, I recommend naming your reposity `[your username].github.io` as this simplifies the URL used to access your tracker in the browser.
2. Ensure your repository is set to **Public**. This is done in the Settings tab of the repository view.
3. Also in the Settings tab of the repository view, you will want to go to the Pages sidemenu item. Select "Deploy from Branch" in Source and then "main" in the Branch dropdown. Hit save. This is what will launch your tracker when you make code updates. You can watch the launching progress in the Actions tab of the repository view (it will show a green checkmark next to the top-most item when it's done). When your site is launched, it will be accessible at one of two URLs, depending on your repository's name: `[account username].github.io` if you named it as recommended above, _or_ `[account username].github.io/[repository name]` if not.

### Initial Setup
1. Ensure all contents of the .zip file are unzipped and uploaded to your GitHub repository.
2. Create a new Google Sheet using [this template](https://docs.google.com/spreadsheets/d/1feZzdIMOgfjJjh4daZTj0wuJHf6bZkDKXLZ1PIr8vdY/edit?usp=sharing).
3. In Google Sheets, click Extensions > Apps Script. It should match the contents of the `googleSheets.txt` in the main folder of the provided coded. If not, replace with the code there.
4. While in Apps Script, click on the `doGet` dropdown. Change this to `setup`. Then, click Run and go through the authentication process. If it claims that 'Google hasn’t verified this app', click through "Advanced > Go to Untitled project (unsafe)" to finish the remaining authentication steps.
5. Click on "Deploy > New Deployment". Ensure "Web App" is selected and that "Who has Access" is set to "Anyone". It will take you through authentication a second time. After, it will provide you a Deployment ID. Copy this and paste it in the `dist/js/settings.js` file within the quotations following `const deployID = `.
6. Go back to your Google Sheet. Change the Share settings so that Anyone with the Link is a Viewer. Then, copy the alphanumeric string from the URL. This string will be immediately after `https://docs.google.com/spreadsheets/d/` and ends immediately before `/edit`. This string needs to be assigned to `sheetID` in the same way the deployment ID was assigned to `deployID` in the last step. For example, the template Google Sheet above would have an ID of `1feZzdIMOgfjJjh4daZTj0wuJHf6bZkDKXLZ1PIr8vdY`;
7. Save and commit the changes to GitHub.
8. Then, use the forms in the Admin portion of your tracker to add sites, character tags, characters, writing partners, and threads. The code should handle most of the rest!

### Adding Site Pages
1. The script will auto-generate the links, but not the new pages. Use the `sample.html` pages within the `/threads`, `/characters`, `/stats`, and `/writing` folders as a template.
2. Find the instances of `site name from sheet` in all three files and replace with a _fully lowercase_ name that _exactly_ matches the site name entered in the Site column of the Sites page from your Google Sheet.
3. Go to `/stats/statuses.html`. Copy and paste the code within `<!-- |Start Site Status Block| -->` and `<!-- |End Site Status Block| -->`, then replace `site name from sheet` as in Step 2 and then `siteidfromsheet` with the matching value from the ID column of the Sites page of your Google Sheet.
4. Save and commit the changes to GitHub.

### Change Thread Tags
1. If you have different thread tags in mind, go to `/dist/js/settings.js`. Find `const threadTags`. Any string assigned inside this array will be added to the forms so that you can add those tags to your threads.
2. Save and commit the changes to GitHub.

### Change Relationship Tags
1. If you have different relationship sections and/or options in mind, go to `/dist/js/settings.js`. Find `const relationshipSections` for sections and `const relationshipOptions` for options. These are just static HTML options inside a JS string, so edit as you would HTML and stay within the backticks and you should be okay! It gets placed within the `<select></select>` tags for you, so do not include those.
2. Save and commit the changes to GitHub.

### Change Chart Colors
1. If you have different chart colors in mind, go to `/dist/js/settings.js`. Find `const chartColors`. Add colors you want inside strings within this array, and remove colors you don't want. The charts will use them in order every time, so put your preferred colors at the start of the array!
2. Save and commit the changes to GitHub.