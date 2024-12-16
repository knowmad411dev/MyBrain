---
Video-URL: https://www.youtube.com/watch?v=7f8e5IiUkeo&list=WL&index=2
tags:
- github
- obsidian
---

## **Obsidian Notes Website for Free

## **Overview**

Callum, also known as Wots, presents a detailed tutorial on how to **publish an Obsidian Vault** as a **digital garden** or **blog website**. He demonstrates using the **Obsidian Digital Garden plugin**, **GitHub**, and **Netlify** (referred to as "nly" in the transcript) to create and host a static website linked to a custom domain. This method is touted as the **easiest and most cost-effective** way to launch a website based on an Obsidian Vault.

---

## **Tools and Services Used**

1. **Obsidian**: A powerful knowledge base tool using Markdown.
2. **Digital Garden Plugin for Obsidian**: Converts Obsidian notes into a static site.
3. **GitHub**: Hosts the repository for the static site.
4. **Netlify**: Hosts the static website.
5. **Namecheap**: Registers a custom domain.
6. **Let's Encrypt**: Provides free SSL certificates for HTTPS.

---

## **Step-by-Step Instructions**

### **1. Setting Up GitHub**

- **Create a GitHub Account**:
    - Visit [GitHub](https://github.com/) and sign up for a new account.
- **Create a Repository**:
    - This repository will store the Markdown files from your Obsidian Vault and facilitate the static site generation.

### **2. Setting Up Netlify**

- **Create a Netlify Account**:
    - Visit [Netlify](https://www.netlify.com/) and sign up, preferably using the same GitHub account for seamless integration.
- **Netlify Free Tier Benefits**:
    - **300 Build Minutes/month**
    - **125,000 Visitors/month**
    - **100 GB Bandwidth/month**
- **Alternative Hosting Providers**:
    - While Netlify is used in the tutorial, alternatives like Vercel and GitHub Pages are also mentioned.

### **3. Installing the Digital Garden Plugin in Obsidian**

- **Install the Plugin**:
    - Open Obsidian.
    - Navigate to `Settings` > `Community Plugins` > `Browse`.
    - Search for **Digital Garden** and install it.
    - Enable the plugin after installation.

### **4. Connecting GitHub to Obsidian's Digital Garden Plugin**

- **Generate a GitHub Personal Access Token**:
    - In GitHub, go to `Settings` > `Developer settings` > `Personal access tokens` > `Tokens (classic)` or **Fine-grained tokens** for better security.
    - **Fine-Grained Token**:
        - Name: `digital-garden`
        - Expiration: 90 days (extendable up to 1 year)
        - Permissions:
            - **Contents**: Read and write
            - **Pull Requests**: Read and write
        - **Repository Access**: Grant access only to the `digital-garden` repository for enhanced security.
- **Authorize in Obsidian**:
    - In the Digital Garden plugin settings, input the generated GitHub token to authenticate.

### **5. Publishing Notes to GitHub and Netlify**

- **Creating and Publishing the Home Note**:
    - Create a new note in Obsidian (e.g., `Digital Garden Home`).
    - Add two properties:
        - `DG Publish`: Checkbox
        - `DG Home`: Checkbox (ensure only one note has this checked to avoid conflicts)
    - Write content for the home page.
    - **Publish the Note**:
        - Press `Command + P` and select `Publish Digital Garden: Single Note`.
        - This action uploads the note to the GitHub repository, triggering Netlify to build and deploy the site.
- **Publishing Multiple Notes**:
    - Similar to publishing a single note, but use the `Publish Multiple Notes` option to batch upload.

### **6. Customizing the Digital Garden**

- **Manage Note Settings**:
    - **Home Link**: Links back to the home note.
    - **Local Graph**: Displays connections between notes.
    - **Backlinks**: Shows notes that link to the current note.
    - **Table of Contents**: Automatically generates navigation based on headers.
    - **Inline Title**: Displays the note title on the page.
    - **File Tree Sidebar**: Provides folder-based navigation.
    - **Search**: Enables site-wide search functionality.
    - **Link Preview**: Hovering over links shows previews of linked notes.
    - **Tags**: Organizes notes into categories.
- **Manage Appearance**:
    - **Site Title**: Customize the website title.
    - **Timestamps**: Show creation and update times for notes.
    - **Custom CSS**: Optional for advanced styling.
    - **Themes**: Choose from various themes (e.g., Aurora Twilight).

### **7. Creating Templates for Consistency**

- **Set Up a Template**:
    - Create a template note with predefined properties (`DG Publish`, `DG Home`, `Tags`, etc.).
    - Use hotkeys (e.g., `Command + Shift + T`) to quickly generate new notes based on this template, ensuring consistency across all published notes.

### **8. Purchasing and Connecting a Custom Domain**

- **Purchase a Domain**:
    - Visit [Namecheap](https://www.namecheap.com/) or any domain registrar.
    - Example: `wanderloot.xyz` for approximately $2.71/year.
- **Configure DNS Settings**:
    - In Namecheap, manage the domain and switch to **Custom DNS**.
    - Obtain Netlify's name servers and update them in Namecheap's DNS settings.
    - **Note**: DNS propagation can take from a few minutes to several hours.

### **9. Enabling HTTPS with Let's Encrypt**

- **Automatic SSL via Netlify**:
    - Netlify integrates with **Let's Encrypt** to provide free SSL certificates.
    - **Steps**:
        - In Netlify, go to `Domain Management`.
        - Add your custom domain (e.g., `wanderloot.xyz`).
        - Follow prompts to verify and connect the domain.
        - Netlify will handle SSL certificate issuance via Let's Encrypt.
- **Manual DNS Record Addition (if necessary)**:
    - Add CAA records to authorize Let's Encrypt:

```plaintext

        Type: CAA Name: wanderloot.xyz Value: 0 issue "letsencrypt.org"
```

    - Repeat for the `www` subdomain:

```plaintext
        Type: CAA Name: www.wanderloot.xyz Value: 0 issue "letsencrypt.org"
```

- **Verification**:
    - After DNS propagation, access your site via `https://wanderloot.xyz` to ensure it's secure.

### **10. Finalizing and Launching**

- **Publish Final Notes**:
    - Continue creating and publishing notes from Obsidian to build out the digital garden or blog.
- **Integration with Other Platforms**:
    - Link the digital garden to other websites or platforms (e.g., a main blog site at `wls.com` and social platforms like `forecaster`).

---

## **Key Web Links Mentioned**

1. **Obsidian**: [https://obsidian.md/](https://obsidian.md/)
2. **Digital Garden Plugin**: Accessible via Obsidian's Community Plugins.
3. **GitHub**: [https://github.com/](https://github.com/)
4. **Netlify**: [https://www.netlify.com/](https://www.netlify.com/)
5. **Namecheap**: [https://www.namecheap.com/](https://www.namecheap.com/)
6. **Let's Encrypt**: [https://letsencrypt.org/](https://letsencrypt.org/)

_Note: Specific URLs for starter guides and documentation were mentioned to be in the video description but are not provided in the transcript._

---

## **Additional Tips and Best Practices**

- **Repository Visibility**:
    - By default, GitHub repositories are public. To maintain privacy, especially for unpublished or private notes:
        - Navigate to the repository's `Settings`.
        - Scroll to the `Danger Zone` and change visibility to `Private`.
- **Security**:
    - Using fine-grained GitHub tokens limits access to specific repositories, enhancing security.
    - Always ensure that only the necessary permissions are granted to third-party applications.
- **Customization**:
    - Utilize custom CSS for advanced styling of the digital garden.
    - Explore different themes within the Digital Garden plugin to personalize the website's appearance.
- **Content Organization**:
    - Use tags and aliases to categorize and link notes effectively.
    - Implement a folder structure in Obsidian to organize notes, which will reflect on the website.

---

## **Conclusion**

Callum's tutorial provides a **comprehensive guide** to transforming an Obsidian Vault into a publicly accessible digital garden or blog. By leveraging free and low-cost tools like GitHub and Netlify, along with the Digital Garden plugin, users can create a customizable and secure website. The inclusion of a custom domain enhances professionalism and brand recognition. This setup not only facilitates the sharing of knowledge but also integrates seamlessly with other content platforms, fostering a cohesive content creation and publication ecosystem.

[[Obsidian]]   [[GitHub]]
