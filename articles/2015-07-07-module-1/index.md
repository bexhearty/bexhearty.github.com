
# Module 1. 

Module 1 (45 Minutes): Make a website and implement Segment from scratch in ten steps. 

1.
Create an account in GitHub (https://github.com/new) or sign in.

2.
Create a new repository (click on the black + sign on the top right) and call it `yourusername.github.io` . In my case, my new repository is called `thebecky.github.io`, check the box that initializes the repo with a README file, and click on the “Create repository” button.
![](https://lh4.googleusercontent.com/7pAUHBkudZZNE-2el-xvBiw847A_KJK4AfIE6J4hcZLOURkFUQO3h3juy6Rbo2Ga9ZcIo4LIiVymliSpjvr-4CVmahvcx9Ttm3kWIi8fvmWgG7pNqRCNcOfcboRvfg2MdjX7Mwk)

3.
Create a new file by clicking on the blue + symbol next to your new repository’s name and call it index.html (this file will contain the code for your website’s default page)

![](https://lh3.googleusercontent.com/2gBmt3YAt1nut9kwvPxr0dEE3H5_1_cweeMmygZIgooQX7ButSFH48Hn4Dj1qADAINgXla6SZt40pl831XghO0nO_ULGgE2l-32nc73nerXnbgHbMc7fo0sd8DWdkL1sjUbYi28)

4.
On that `index.html` file, insert the following text, and commit that file by clicking on the green "Commit” button:

```html 
<!DOCTYPE html>
        <html>
        <head>
                <title>Travel Destinations</title>
                <!--Placeholder for Segment Snippet -->
                <!--Placeholder for index.css link -->
        </head>
        <body>
        <nav>
        <ul>
                <li><a href="/">Home</a></li>
                <li><a href="/countries">Countries</a></li>
                <li><a href="/blog">Blog</a></li>
        </ul>
        </nav>
        <div class="container">
        <div class="blurb">        
        <h1>What is your favorite place to travel?</h1>
                <p>I am building a directory of the sweetest travel destinations.</p>
                <br><br>
                <form name="travel" onsubmit="identify(event)">
                Favorite Travel Destination:
                <br><br>
                <input name="destination" required="" size="81" type="text"/>
                <br><br><br>
                Cool things to do, places to see and restaurants to visit:
                <br><br>
                <textarea cols="81" name="details" required="" rows="10"></textarea>
                <br><br>
                Name:
                <input name="fullname" required="" size="75" type="text"/>
                <br><br>
                Email:
                <input name="email" required="" size="75" type="email"/>
                <br><br><br>
                <input name="submit" type="submit" value="submit" style="color: #ffffff; background: #63686b; font-size: 1em; border: none;"/>
                <br><br>
                </form>        
        /form> 
        </div>
        </div>
        <footer>
        <ul>
               <li><a href="mailto:beckyjaimes@gmail.com">email me</a></li>
        </ul>
        </footer>
        </body>
        </html>
```

5.
On a separate window, navigate to  yourusername.github.io. There you should be able to see your new website (it might take up to 5 minutes). Should look ugly like this:

![](https://lh4.googleusercontent.com/htMHBgB6SmAWH98_kNRSV6SpmImYisWdAcGcyRnOma1FH30C208_qo1MRMWtKIzM0Re_LK5MawP0dwX2Dg6NgjgEsbVxmexI6nIzK1Z0jaYGvVOKcjMhrMEfhRqDCbopFP5KpM0)

6.
To make it pretty,  create an `index.css` file. Insert the following text on that file, and press the green commit button:

```
body {
    font-family: 'Helvetica', 'Arial', 'Sans-Serif';
    font-size:1em;
    margin: 60px auto;
    width: 70%;
}
nav ul, footer ul {
    font-family:'Helvetica', 'Arial', 'Sans-Serif';
    padding: 0px;
    list-style: none;
    font-weight: bold;
}
nav ul li, footer ul li {
    display: inline;
    margin-right: 20px;
}
a {
    text-decoration: none;
    color: #999;
}
a:hover {
    text-decoration: underline;
}
h1 {
    font-size: 2em;
    font-family:'Helvetica', 'Arial', 'Sans-Serif';
}
p {
    font-size: 1.1em;
    line-height: 1.4em;
    color: #333;
}
footer {
    border-top: 1px solid #d5d5d5;
    font-size: .8em;
}

ul.posts { 
    margin: 20px auto 40px; 
    font-size: 1.5em;
}

ul.posts li {
    list-style: none;
}

img {
  display: block;
  max-width: 100%;
}
```

Your project code should now look like this: 
![](https://lh6.googleusercontent.com/WElic7ObgxtawSB7YpoMqwRQYxxORQT6vKz62p5XcCuPP2kJ19ac59at2LPC8Vood63_9W81oB7GwDjnlHnRBR_USO1EQdyh5jKg7cyXmIMMyJnUtqCq__MvFZkYg-KzpIv-cOY)

7.
Go back to the first file we created, the `index.html` file, click on the pencil on the top right (to edit) and replace the text that reads `<!--Placeholder for index.css link -->` in line 6  with `<link rel="stylesheet" href="/index.css">`. The new file should look like this:

![](https://lh6.googleusercontent.com/Bipyrmp-mMQrgwTkRS_ZEkDm8mLjXG7J_LusLIx8thjRvW6Waua6Ng3HwyJmYnrluoruoTOlSlRGOFIQUs8Xq_7DWSCXgcjKJQJeWGITTEutoMDOk7K8dekiYaRGKYNwsqcxI08)

After committing the change, and refreshing your `yourusename.github.io` website, it should be stylin like this:
![](https://dchtm6r471mui.cloudfront.net/notes.dropbox.com_2KqZoOTMGXjhQh7myTv8k_d.2308_1436279269707_undefined)

8.
Segment on your site. 
First create a Segment project and click on the “install a library in your site or mobile app” option (or select it by clicking on the 6th icon called “setup project”)

![](https://lh6.googleusercontent.com/ue6swDWFchY5LllpF-fw60ig5peul0A7eYrMEeP-euZz9BnfSekldy1jwHL_bBjjKyI3Fec-ReOE9NxoJjC1YIdpO5g5twfIEdP5ycdsJMiSEC6Yn8jqHdUZUf5RMRF6v2EeIdI)

Copy the full snippet from the box on your segment dashboard, go back to your `index.html` file, select the pencil to edit, and replace the line that reads `<!--Placeholder for Segment Snippet -->` (mine is line 5) with the Segment snippet.

Your new file should look like this:
![](https://dchtm6r471mui.cloudfront.net/notes.dropbox.com_2KqZoOTMGXjhQh7myTv8k_d.2308_1436248776313_undefined)

9.
Identify those users that submit a destination. To do so, create a little function that captures the input from the form, and sends some of that data as parameters in an identify call. While we are at it, lets also send an event using the .track method called “destination submitted.”  We are going to do that on the same index.html file, so if you haven’t committed your changes yet (if you have, just open to edit the index.html file again), scroll down to the line after the </form> (mine is line 44) and insert the following text.
```   
<script type="text/javascript">
        function identify(e){
        e.preventDefault();
        var form = e.target;
        var email = form["email"].value;
        var fullname = form["fullname"].value;
        var destination = form["destination"];
        var details = form["details"].value;
        var user = {email: email, name: fullname, details: details};
        analytics.identify(email, {email: email, name: fullname});
        analytics.track('destination submitted', user, function() {
            window.location.href = "/blog";
        });
        }
</script>
```
Your index.html file should contain code similar to the one found here (with your project’s Segment write key in line 7).

10.
Commit the changes. Go back to your website and submit a travel recommendation form.
![](https://lh6.googleusercontent.com/XwmCdFqs7yF7nMYndphwPR_kyPoMVQipuUedClecnF9tjO5rh5XG77wpqa7C4znkBkBHJhN8vv2q9qSHwSewIqgTV3b-Nn0lmh8AFtAvxCYs1K2EMVKM2YwK3AmSNPUBcXQ4tvg)

Go back to your site’s debugger on the Segment’s dash. You should be able to see the following 3 calls:

![](https://dchtm6r471mui.cloudfront.net/notes.dropbox.com_2KqZoOTMGXjhQh7myTv8k_d.2308_1436278764869_undefined)

Wouldnt it be nice that the page call had the actual title of the page? To make that happen, simple replace `analytics.page()` in your index.html file (mine is in line 8) with  `analytics.page(document.title)`.

your calls should now look like this:

![](https://dchtm6r471mui.cloudfront.net/notes.dropbox.com_2KqZoOTMGXjhQh7myTv8k_d.2308_1436279711665_undefined)

Congratulations! You just finished Module 1 of this training series.

One thing worth pointing out is that for simplicity purposes we didn’t follow Segment’s best practices when assigning a random userID for each user. Instead, we sent our user’s email address as the userID and that will not make Sperandio proud. The reason that sending the email is less than ideal, is because users can have many email addresses and we dont want to count one user multiple times.

What is in **Module 2**?   Notice how after submitting your form you were taken to a 404 page. That is because we redirected the user after pressing the “submit” button to the website’s blog (yourusername.github.io/blog) - but we haven’t created one yet! In module 2 we will create a blog page and a countries page using Jekyll.
We will also integrate with Optimizely and Keen. Optimizely is an interesting one, as it only integration that requires their snippet to also be loaded into our page.