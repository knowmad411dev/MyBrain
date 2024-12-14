---
Video-URL: https://www.youtube.com/watch?v=7f8e5IiUkeo&list=WL&index=4
tags:
- web
- obsidian
---

## **Obsidian on Digital Garden

### How to Publish Your Obsidian Vault as a Digital Garden

The tutorial by Callum (also known as Wots) demonstrates how to turn an Obsidian vault into a public-facing digital garden or blog using a plugin for Obsidian and free or low-cost tools like GitHub and Netlify. This guide enables users to create a static website from their Obsidian notes and connect it to a custom domain. The process involves setting up three main components: Markdown files (managed in Obsidian), a static site generator (the Obsidian Digital Garden plugin), and hosting (using Netlify).

### Key Components and Steps to Create a Digital Garden

1. **Preparation and Philosophy**

    - **Markdown & Obsidian:** Markdown files in Obsidian are used as the base content for the website.
    - **Static Site Generator (SSG):** The Obsidian Digital Garden plugin utilizes [11ty (Eleventy)](https://www.11ty.dev/), a static site generator, to convert Markdown files into a static HTML site.
    - **Hosting:** Netlify, a free hosting provider, is used to host the static website. Alternatives like Vercel and GitHub Pages are mentioned, but Netlify is preferred due to its generous free tier and ease of use.
2. **Setting Up a GitHub Account**

    - A GitHub account is required as it stores the repository that the Obsidian Digital Garden plugin will use to generate the site.
    - After creating an account, you also create a repository for the digital garden.
3. **Setting Up Netlify**

    - **Netlify Account:** Sign up for a Netlify account using GitHub for easier integration.
    - **Netlify's Free Tier:** Allows for up to 300 build minutes per month, 125,000 visitors, and 100 GB of bandwidth. For most users using Markdown, this should be sufficient.
    - **Alternative Hosting Providers:** Vercel is mentioned as an alternative but has some limitations on daily changes.
4. **Install the Obsidian Digital Garden Plugin**

    - In Obsidian, go to the settings, find the Community Plugins, and install the Digital Garden plugin.
    - Follow the documentation available on the [Digital Garden GitHub page](https://github.com/oleeskild/obsidian-digital-garden) for additional guidance.
5. **Connect the GitHub Account to Obsidian**

    - Use a GitHub access token to authorize Obsidian to publish content to the GitHub repository.
    - **Fine-grained Tokens vs. Classic Tokens:** Fine-grained tokens are recommended as they provide more secure, repository-specific access.
    - Once authenticated, the plugin is ready to publish notes to GitHub.
6. **Publish Your First Note**

    - Create a note in Obsidian, and set the frontmatter properties `dg-publish` and `dg-home`. `dg-home` designates the note as the homepage of the digital garden.
    - To publish, use the plugin command: `Publish Digital Garden > Publish single note`. The note will be sent to GitHub and built on Netlify.
    - You can view the newly deployed site on the Netlify domain.
7. **Configure Repository Settings**

    - **Visibility Settings:** Change your GitHub repository from public to private to prevent unauthorized access to your notes.
8. **Customizing Appearance and Features**

    - **Digital Garden Settings:** Customize the look and features of your website:
        - **Home Link, Graph View, Backlinks, Table of Contents, and Search.**
    - **Appearance and Themes:** Set a site title, timestamps for creation and update, and choose from a variety of themes to personalize your site. For example, "Aora Twilight."
    - **Custom CSS:** Advanced users can introduce custom CSS to style the website further.
9. **Automate Note Properties with Templates**

    - Create a template in Obsidian with properties like `dg-publish` and any additional metadata, such as tags or aliases, to quickly format new notes before publishing them.
    - **Hotkeys for Efficiency:** Assign a hotkey to insert the template quickly into any new note.
10. **Custom Domain Setup**

    - **Buy a Domain Name:** Use a domain registrar like [Namecheap](https://www.namecheap.com/) to buy a domain. Namecheap offers competitive pricing, and optional SSL can be purchased to secure the site.
    - **Connect Domain to Netlify:** Go to Netlify’s domain management and add your custom domain. Then update your domain's DNS settings on the registrar’s website (e.g., Namecheap) to point to Netlify's name servers.
    - **DNS Propagation:** DNS changes can take anywhere from a few minutes to a couple of days to propagate.
11. **Enable HTTPS**

    - **Free HTTPS with Let's Encrypt:** Netlify supports free SSL/TLS through [Let's Encrypt](https://letsencrypt.org/). Once the CAA DNS record is set up, Netlify will handle the certificate issuance.
    - No need to purchase SSL separately when using Netlify and Let's Encrypt.
12. **Content Publishing Workflow**

    - **Regular Updates:** Create new notes, set `dg-publish`, and publish them through the plugin to have them appear on the site.
    - **Digital Garden vs. Blog:** The digital garden allows for connected thoughts and a knowledge graph to explore relationships between notes, while a blog is more linear and article-focused.

### Additional Resources & Further Customization

- Explore additional features and settings within the Digital Garden plugin FAQ and documentation for further customization of your digital garden.
- **Expand Functionality:** Use backlinks, tags, DataView queries, and CSS tweaks to make the site your own.

### Key Links

1. **Obsidian Digital Garden Plugin Repository:** [GitHub Link](https://github.com/oleeskild/obsidian-digital-garden)
2. **Eleventy Static Site Generator (11ty):** [Website](https://www.11ty.dev/)
3. **Netlify:** [Website](https://www.netlify.com/)
4. **Domain Registrar (Namecheap):** [Website](https://www.namecheap.com/)
5. **Let’s Encrypt for HTTPS:** [Website](https://letsencrypt.org/)

### Code & Command Summary

- **Frontmatter Properties for Publishing:**

```yaml
    --- dg-publish: true dg-home: true  # only for home page note ---
```

- **Publishing Commands in Obsidian:**
    - `Publish Digital Garden > Publish single note` (publishes a single note).
    - `Publish Digital Garden > Publish multiple notes` (publishes multiple notes).
    - Use a template with predefined properties and use a hotkey for quick application.

[[Obsidian]]   [[GitHub]]  [[Obsidian Notes Website for Free]]
