# FalekMiah-Blog

This repository contains objects and blogs relating to blog website.


## **Development Steps**

<br>

### **Develop in VSCode**

Add New Content Blog Page:
   1) Add blog `content` into a new file under folder *`...\content\english\blog'`*
   2) Add blog `images` into folder  *`'...\static\images'`*
   3) Add blog `images` using HTML. 
       - Update `image URL` in blog to use `forward slash (/)` and **not** backward slash (\).
   4) Add blog `portfolio` into a new file under folder *`'\content\english\portfolio\'`*

<br>
    
Example HTML code for image:

```html
<a  href="/images/portfolio/<folderName>/<fileName>.png" target="_blank">
<img src="/images/portfolio/<folderName>/<fileName>.png" alt="<description>" width="800" align="center"></a>
```
 
<br><br>
     
### **Local Testing**
Test locally in VSCode using the Development Server and Hugo commands. 
 
| **Command**                      | **Description**                                   |
| -------------------------------- | ------------------------------------------------- |
| hugo  server                     | Start  Hugo’s development server to view the site |
| hugo  version                    | Get  version                                      |
| hugo  new posts/my-first-post.md | Add a  new page                                   |
|                                  |                                                   |

<br><br>

## **Deployment Steps**

<br>

### **Deploy Website using GitHub Actions**

Deploy to Website:
   1) Push Feature Branch into GitHub
   2) Merge branch using a PR
   3) CI/CD on GitHub Actions should automatically trigger
   4) Check website
