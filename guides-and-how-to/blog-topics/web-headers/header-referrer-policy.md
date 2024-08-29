## **Referrer-Policy: A Developer’s Guide to Controlling Referrer Information**

### **Introduction**

In the complex web ecosystem, every time a user clicks a link to navigate from one page to another, their browser may send referrer information to the destination page. This information can include the URL of the previous page, which can sometimes reveal sensitive data. The Referrer-Policy header is a vital tool for developers to control what referrer information is shared when users navigate between sites. This guide will introduce you to the Referrer-Policy header, explain its significance, and walk you through its implementation.

### **What is Referrer-Policy?**

The Referrer-Policy header is a security feature that governs how much referrer information is sent along with requests made from your web pages. The referrer information typically includes the full URL of the previous page, which can inadvertently expose sensitive data such as query parameters or fragment identifiers. 

By using the Referrer-Policy header, you can limit the amount of referrer information that gets shared, thereby enhancing user privacy and protecting sensitive information from being unintentionally disclosed.

### **Why is Referrer-Policy Important?**

When users navigate between pages on your site or to external sites, the referrer information sent can sometimes expose more than intended. For example, if a user is on a page with a URL like `https://your-site.com/search?q=sensitive-term`, this full URL might be sent as the referrer to the next site, revealing the search term. In some cases, this could lead to privacy issues or even security risks.

The Referrer-Policy header allows you to take control of what referrer data is shared, helping you protect user privacy, meet compliance requirements, and pass security audits that flag unnecessary exposure of referrer information.

### **How Does Referrer-Policy Work?**

The Referrer-Policy header works by setting a policy for how much of the referrer information should be included with outgoing requests from your site. Depending on your needs, you can choose to send the full referrer, a reduced version, or none at all.

### **Implementing Referrer-Policy: A Step-by-Step Guide**

Implementing the Referrer-Policy header is straightforward and can significantly improve your site's privacy controls. Here's how you can add this header to your web server configuration.

#### **1. Understanding the Header Values**

The Referrer-Policy header supports several values that dictate what referrer information is sent with requests:

- **no-referrer:** Sends no referrer information at all.
- **no-referrer-when-downgrade:** Sends the referrer for HTTPS requests but omits it when navigating to a less secure HTTP page.
- **origin:** Sends only the origin (e.g., `https://your-site.com`) of the referrer URL, omitting the path and query parameters.
- **origin-when-cross-origin:** Sends the full referrer for same-origin requests but only the origin for cross-origin requests.
- **same-origin:** Sends the full referrer for requests within the same origin but no referrer for cross-origin requests.
- **strict-origin:** Sends only the origin for HTTPS requests and no referrer when navigating to a less secure HTTP page.
- **strict-origin-when-cross-origin:** Combines the behavior of `strict-origin` and `origin-when-cross-origin`, sending the origin for cross-origin requests over HTTPS and no referrer when downgrading to HTTP.
- **unsafe-url:** Sends the full referrer for all requests, regardless of security implications.

**Examples:**

```http
Referrer-Policy: no-referrer
```

```http
Referrer-Policy: origin-when-cross-origin
```

```http
Referrer-Policy: strict-origin-when-cross-origin
```

#### **2. Choosing the Right Policy**

Selecting the appropriate Referrer-Policy depends on your specific needs. If privacy is a primary concern, `no-referrer` or `strict-origin` are good choices. If you need to balance privacy with functionality (e.g., analytics or debugging), `origin-when-cross-origin` or `strict-origin-when-cross-origin` might be more suitable.

#### **3. Configuring Referrer-Policy in Apache**

For Apache users, you can set the Referrer-Policy header in your site’s configuration file (`/etc/apache2/sites-available/your-site.conf`) or in the `.htaccess` file:

```apache
<IfModule mod_headers.c>
    Header set Referrer-Policy "strict-origin-when-cross-origin"
</IfModule>
```

After adding this directive, restart Apache to apply the changes:

```bash
sudo systemctl restart apache2
```

#### **4. Configuring Referrer-Policy in Nginx**

For Nginx, add the header to your site’s configuration file (`/etc/nginx/sites-available/your-site.conf`):

```nginx
add_header Referrer-Policy "origin-when-cross-origin";
```

Then, restart Nginx to apply the changes:

```bash
sudo systemctl restart nginx
```

#### **5. Testing the Header**

Once configured, you can test the Referrer-Policy header using browser developer tools or by making requests with cURL:

```bash
curl -I https://your-domain.com
```

Check the response headers to confirm the `Referrer-Policy` is correctly applied.

### **Best Practices for Using Referrer-Policy**

To effectively use the Referrer-Policy header, consider these best practices:

- **Minimize Exposure:** When in doubt, choose a policy that reduces the amount of referrer information shared, such as `strict-origin` or `no-referrer`.
- **Evaluate Business Needs:** While privacy is crucial, balance it with any business needs for analytics or functionality that might require some referrer information.
- **Test Thoroughly:** Ensure your chosen policy does not unintentionally break any functionality, especially if your site relies on referrer data for analytics or other purposes.
- **Stay Updated:** As browsers and web standards evolve, review your Referrer-Policy settings regularly to ensure they remain optimal.

### **Addressing Audit Findings with Referrer-Policy**

Security audits often highlight the unnecessary sharing of referrer information as a privacy concern. Implementing a Referrer-Policy helps you address these findings by controlling the referrer data that is sent from your site, thus enhancing user privacy and meeting compliance standards.

By setting a clear and appropriate Referrer-Policy, you not only resolve potential privacy issues but also show a commitment to safeguarding user data. This proactive approach is crucial for maintaining user trust and passing security audits with flying colors.

### **Conclusion**

The Referrer-Policy header is an essential tool for managing the privacy and security of your web application. By controlling what referrer information is shared, you protect sensitive data and ensure that your users' interactions with your site are secure.

As a developer, implementing the Referrer-Policy header is a simple yet powerful step towards building a more secure web. By carefully choosing and applying the right policy, you can safeguard user privacy while maintaining the functionality of your application. Keep learning, keep refining your security practices, and continue to create web applications that not only perform well but also protect the data and trust of your users.