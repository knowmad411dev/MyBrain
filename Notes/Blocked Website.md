---
tags:
- web
video-url: https://www.youtube.com/watch?v=EB2gn9G9sV8&list=WL&index=13
---

## **Blocked Website**

The video "They know you're using Browser Automation, so try this" on YouTube discusses how websites can detect browser automation tools like Playwright, Puppeteer, and Selenium, and offers solutions to avoid detection for web scraping and automation purposes. Here's a detailed summary, including referenced websites, how-to instructions, and relevant code.

### Key Concepts Covered:

1. **Browser Fingerprinting**: Websites can identify browsers through various characteristics such as system fonts, screen resolution, graphics rendering, time zone, IP address, and more. Tools like **PixelScan.net** and **BrowserLeaks.com** can be used to check how much information your browser reveals.
2. **IP Address and Location Matching**: The video emphasizes the importance of matching your system’s location with the proxy location during automation. Mismatches between your IP address and other indicators, like time zone, can lead to detection and blocking by websites.
3. **Proxies**: The presenter recommends using high-quality proxies to prevent being blocked when automating web scraping. He suggests using services like **ProxyScrape**, which offer rotating and sticky session proxies, including residential, data center, and mobile proxies. Using location-targeted proxies can improve your chances of passing antibot protections.
4. **Automation Detection**: Tools like Playwright, Puppeteer, and Selenium can be detected by websites using JavaScript, especially by checking the `navigator.webdriver` flag. If this flag is set to `true`, it indicates that a browser automation tool is running.

### Techniques to Avoid Detection:

1. **Handling** `**navigator.webdriver**` **Flag**:

    - Websites check the `navigator.webdriver` property to see if automation is being used. If it returns `true`, they block access.
    - By using certain packages and modifying the browser's behavior, you can prevent this flag from being detected.

    Code example:

    ```
    console.log(navigator.webdriver);  // returns true if automation is detected
    ```

    The video demonstrates how this can be bypassed by altering the browser's fingerprint.

2. **Screen Resolution & User Agent**:

    - Uncommon screen resolutions or obvious user agents like "Headless Chrome" can trigger antibot systems. Ensure that the user agent and screen resolution appear as they would in a natural browsing session.

    Example of how Playwright might expose automation:

    ```
    const { chromium } = require('playwright');
    (async () => {
        const browser = await chromium.launch({ headless: false });
        const page = await browser.newPage();
        await page.goto('https://pixelscan.net');
    })();
    ```

    The video highlights the importance of using tools that hide these identifiers effectively.

3. **Selenium Base & Undetected ChromeDriver**:

    - A more advanced approach discussed in the video is using **SeleniumBase** with the "undetected Chrome driver" (UC mode), which helps avoid automation detection. This tool patches the usual flags like `navigator.webdriver` and modifies other Chrome DevTools variables that give away the use of automation.

    Code example for running SeleniumBase in UC mode:

    ```
    from seleniumbase import BaseCase
    
    class MyTestClass(BaseCase):
        def test_automation_detection(self):
            self.open("https://pixelscan.net")
            self.assert_no_text("Automation detected", "body")
    ```

    The speaker recommends SeleniumBase’s UC mode for avoiding detection and explains that it helps get around most basic checks used by websites.

4. **Websites Mentioned**:

    - [**PixelScan**](https://pixelscan.net/): Useful for checking browser fingerprinting details like fonts, canvas rendering, and automation flags.
    - [**BrowserLeaks**](https://browserleaks.com/): Provides comprehensive information about browser leaks and fingerprinting, including WebRTC leaks, screen resolution, and system details.

### Practical Recommendations:

1. **Proxy Matching**: Always ensure that your system and proxy locations match to avoid detection from location mismatches. High-quality, location-based proxies are vital for evading detection.
2. **SeleniumBase with UC Mode**: If tools like Playwright or Puppeteer fail to bypass detection, SeleniumBase with UC mode is recommended. It addresses many common detection methods and automatically adjusts flags like `navigator.webdriver`.
3. **Avoid Running in Headless Mode**: If you're blocked using headless mode, try running your browser in headful (non-headless) mode to appear more like a normal user.
4. **Use of Undetected Browsers**: There are also paid "undetected browsers" that try to stay ahead of detection methods by continually patching automation-detecting techniques.

### Ethical Disclaimer:

While the video discusses bypassing antibot mechanisms, the presenter advises against using these techniques for malicious purposes, like bypassing CAPTCHA or accessing restricted sites. The focus is on collecting publicly available data for legitimate use cases like data analysis.

### Conclusion:

To effectively bypass browser automation detection for web scraping or automated tasks:

- Use high-quality proxies with proper location matching.
- Bypass automation detection methods such as `navigator.webdriver` by utilizing SeleniumBase with UC mode or similar tools.
- Avoid suspicious screen resolutions and user agents.
- Regularly test your setup using fingerprinting tools like PixelScan and BrowserLeaks.

For more details and to access the resources mentioned, visit:

- [PixelScan](https://pixelscan.net/)
- [BrowserLeaks](https://browserleaks.com/)
- [ProxyScrape](https://proxyscrape.com/)

[[Cloud]] [[Web Scrapping]]