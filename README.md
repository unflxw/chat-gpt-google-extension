# ChatGPT for Firefox

A Firefox extension to show ChatGPT response in Google search results

![Screenshot](screenshot.jpg?raw=true)

## Installation

### Build from source

1. Clone the repo
2. Install dependencies with `npm`
3. Run `./build.sh`
4. Load the `manifest.json` file to Firefox:
  1. Go to `about:debugging`
  2. Select "This Firefox", then "Load Temporary Add-on..."

## Credit

This project was created by @wong2 as a Chrome extension ([wong2/chat-gpt-google-extension](https://github.com/wong2/chat-gpt-google-extension)), and ported to Firefox by ChatGPT, with occasional help from me as a human file system interface, GitHub operator and README writer.

This project is inspired by [ZohaibAhmed/ChatGPT-Google](https://github.com/ZohaibAhmed/ChatGPT-Google)

## Ported by ChatGPT

This is a fork of @wong2's ChatGPT Google extension, ported to Firefox by someone who's never written a browser extension before and who was too tired to read a JSON Schema meta-regex validation error, by asking ChatGPT how to do it. It took me, like, twenty minutes. Here's the conversation between me and ChatGPT:

> **Me:** What are the main steps and hurdles in porting a Chrome extension so that it works with Firefox?

> **ChatGPT:** In order to port a Chrome extension to Firefox, you will need to follow these steps:
> 
> 1. First, you will need to obtain the source code of the Chrome extension. This can usually be done by visiting the Chrome Web Store and downloading the extension as a ZIP file.
> 2. Next, you will need to modify the extension's manifest file to make it compatible with Firefox. The manifest file is a JSON-formatted file that contains important information about the extension, such as its name, version, and permissions. You will need to update the manifest to use Firefox-specific APIs and add any necessary permissions.
> 3. After updating the manifest, you will need to modify the extension's code to use Firefox-specific APIs and functions. This will likely involve making changes to the extension's JavaScript and HTML files.
> 4. Finally, you will need to test the extension to ensure that it works as expected in Firefox. This can be done by installing the extension in a Firefox browser and using it to verify that it functions properly.
> 
> Some of the main hurdles that you may encounter when porting a Chrome extension to Firefox include:
> 
> - Differences in APIs and functions: Chrome and Firefox use different APIs and functions for certain tasks, so you will need to update the extension's code to use the appropriate Firefox-specific APIs and functions.
> - Permission differences: Chrome and Firefox have different permissions systems, so you will need to update the extension's manifest to request the necessary permissions in Firefox.
> - Compatibility issues: Even after making the necessary code and manifest changes, the extension may still not work properly in Firefox due to compatibility issues. This can be due to differences in the way that the two browsers handle certain tasks, or it may be due to bugs or other issues with the extension itself.
> 
> [... blabbery omitted]


> **Me:** Here's the manifest for the Chrome extension:
>
> _[full original manifest.json contents, in a code block]_
> 
> How would you modify it to make it work with Firefox?

> **ChatGPT:**
> To make this Chrome extension work with Firefox, you would need to make the following modifications to its manifest file:
> 
> 1. Change the value of the manifest_version property from 3 to 2. Firefox uses version 2 of the manifest file format, so this change is necessary to make the manifest compatible with Firefox.
> 2. Update the host_permissions property to request the appropriate permissions in Firefox. In Firefox, the host_permissions property is called permissions, and it uses a different format than the Chrome version. For example, the host_permissions property in the Chrome extension above would need to be updated to look like this in Firefox:
> ```
> "permissions": ["https://*.openai.com/"]
> ```
> 3. Update the content_scripts property to use Firefox-specific APIs and functions. In the Chrome version of the manifest above, the content_scripts property specifies a service_worker and include_globs property, which are not supported in Firefox. These would need to be removed from the manifest and replaced with Firefox-specific properties, such as run_at and matches, which are used to specify when and where the content script should be injected.
> 
> For example, the content_scripts property in the Chrome extension above would need to be updated to look like this in Firefox:
> ```
> "content_scripts": [
>     {
>       "matches": ["https://*.google.*/search*"],
>       "run_at": "document_end",
>       "js": ["content-script.js"],
>       "css": ["styles.css"]
>     }
>   ]
> ```
> [... blabbery omitted]


> **Me:** Is there anything else that needs to be done to the manifest?

> **ChatGPT:** In general, there may be other modifications that need to be made to the manifest file in order to make a Chrome extension work with Firefox. These modifications will depend on the specific requirements of the extension, as well as any differences between the Chrome and Firefox extension systems.
> 
> For example, some other modifications that may need to be made to the manifest file include:
> - Updating the name and description properties to use values that are appropriate for Firefox.
> - Adding any additional properties that are required by Firefox but not supported by Chrome, such as the applications property, which is used to specify details about the extension's compatibility with different versions of Firefox.
> - Removing any Chrome-specific properties that are not supported by Firefox, such as the browser_action and page_action properties, which are used to specify the extension's toolbar icon and popup window.
> - Adding any additional permissions that are required by the extension in order to function properly in Firefox.
> 
> [... blabbery omitted]

> **Me:** What permissions are needed to access and modify the contents of the current page?

> **ChatGPT:** If an extension needs to access and modify the contents of the current page in Firefox, it will need to request the activeTab permission in the manifest file. This permission allows the extension to access and modify the content of the current tab, and it is required in order to perform these types of actions.
> 
> To request the activeTab permission, you would need to add the following line to the permissions property in the manifest file:
> 
> "permissions": ["activeTab"]
> 
> It is important to note that the activeTab permission is considered a high-risk permission, as it allows the extension to potentially make significant changes to the content of the current tab.
> 
> [... blabbery omitted]


> **Me:** Can you show me what the manifest would look like, after adding the `activeTab` permission and modifying the other values as you described earlier?

> **ChatGPT:** Here is an example of what the manifest file for the Chrome extension described earlier might look like after adding the activeTab permission and making the other modifications needed to make it compatible with Firefox:
>
> _[full current manifest.json contents, in a code block -- modulo the issue discussed below]_
> 
> In this example, the manifest_version property has been updated to use the correct value for Firefox (2), the host_permissions property has been renamed to permissions and updated to include the activeTab permission, and the content_scripts property has been modified to use Firefox-specific properties and values. Additionally, the applications property has been added to specify compatibility with Firefox.
> 
> [... blabbery omitted]

> **Me:** Perfect, thanks! You also mentioned that the extension's code would need to be modified. Here's the contents of `content-script.js`:
>
> _[full current content-script.json contents, in a code block]_

> **ChatGPT:** In order to make the content-script.js file compatible with Firefox, you would need to make the following modifications:
> 1. Replace any instances of chrome.runtime.connect() with browser.runtime.connect(). In Firefox, the chrome.runtime API is replaced by the browser.runtime API, so any references to chrome.runtime in the code will need to be updated to use the correct API.
> 
> [... three more bullet points of nonsensical modification suggestions, and blabbery, omitted]

> **Me:** How do I install a Firefox extension from its source code?

> **ChatGPT:** To install a Firefox extension from its source code, you will need to follow these steps:
> 1. Download the source code for the extension and unzip it to a local directory on your computer.
> 2. Open Firefox and navigate to the about:debugging page.
> 3. Click the "Load Temporary Add-on" button and select the manifest file for the extension (usually named manifest.json) from the local directory where you unzipped the source code.
> 4. The extension will be installed in Firefox and will be available until you restart the browser.
> 5. To use the extension, click the "Debug" button next to the extension in the about:debugging page, or open the extension's options page if it has one.
> 6. To permanently install the extension, click the "Install" button next to the extension in the about:debugging page. This will add the extension to your list of installed extensions, and it will remain installed even after you restart the browser.
> 
> [... blabbery omitted]

> **Me:** I'm getting this error when loading the manifest:
> ```
> Extension is invalid
> 
> Reading manifest: Error processing content_scripts.0.matches.0: Value "https://*.google.*/search*" must either: be one of ["<all_urls>"], must either [match the pattern /^(https?|wss?|file|ftp|\*):\/\/(\*|\*\.[^*/]+|[^*/]+)\/.*$/, or match the pattern /^file:\/\/\/.*$/], or match the pattern /^resource:\/\/(\*|\*\.[^*/]+|[^*/]+)\/.*$|^about:/
> ```

> **ChatGPT:** This error indicates that the content_scripts.0.matches.0 property in the manifest file is using an invalid value. In this case, the value "https://\*.google.\*/search*" is not allowed by Firefox, because it does not match any of the supported patterns for URL patterns in Firefox extensions.
> 
> To fix this error, you will need to update the content_scripts.0.matches.0 property to use a supported URL pattern. In general, the supported patterns are:
> - "<all_urls>": This pattern matches all URLs, allowing the content script to run on all pages.
> - "http://\*/\*" or "https://\*/\*": These patterns match all URLs that use the http or https scheme, respectively. They allow the content script to run on pages that use these schemes, but not on pages that use other schemes (such as file or ftp).
> - "http://example.com/\*" or "https://example.com/\*": These patterns match all URLs on the example.com domain that use the http or https scheme, respectively. They allow the content script to run on pages on the specified domain, but not on pages on other domains or pages that use other schemes.
> 
> [... blabbery omitted]
