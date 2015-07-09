
# Build a single page website and implement Segment from scratch in nine steps. 
Completion time 45 minutes

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
        <!--Placeholder for Google Analytics Snippet -->
        <!--Placeholder for MixPanel Snippet -->
        <!--Placeholder for KissMetrics Snippet -->
        <!--Placeholder for Segment Snippet -->
        <!--Placeholder for index.css link -->
</head>
<body>    
<br>
<h1>What is your favorite place to travel?</h1>
        <p>I am building a directory of the sweetest travel destinations.</p>
        <br><br>
        <form name="travel" onsubmit="identify(event)">
        What is your favorite travel destination?
        <br><br>
        <input name="destination" required="" size="81" type="text"/>
        <br><br><br>
        Any reccomendations (cool things to do, places to visit or restaurants to eat)?
        <br><br>
        <textarea cols="81" name="details" required="" rows="10"></textarea>
        <br><br>
        Name:
        <input name="fullname" required="" size="75" type="text"/>
        <br><br>
        Email:
        <input name="email" required="" size="75" type="email"/>
        <br><br><br>
        <input name="submit" type="submit" value="submit"/>
        <br><br>
        </form>       
</body>
</html>
```

5.
On a separate window, navigate to  yourusername.github.io. There you should be able to see your new website (it might take up to 5 minutes). Should look similar to this:

![](https://lh4.googleusercontent.com/htMHBgB6SmAWH98_kNRSV6SpmImYisWdAcGcyRnOma1FH30C208_qo1MRMWtKIzM0Re_LK5MawP0dwX2Dg6NgjgEsbVxmexI6nIzK1Z0jaYGvVOKcjMhrMEfhRqDCbopFP5KpM0)


6.
Segment on your site. 
Create a Segment project and click on the “install a library in your site or mobile app” option (or select it by clicking on the 6th icon called “setup project”)

![](https://lh6.googleusercontent.com/ue6swDWFchY5LllpF-fw60ig5peul0A7eYrMEeP-euZz9BnfSekldy1jwHL_bBjjKyI3Fec-ReOE9NxoJjC1YIdpO5g5twfIEdP5ycdsJMiSEC6Yn8jqHdUZUf5RMRF6v2EeIdI)

Copy the full snippet from the box on your segment dashboard, go back to your `index.html` file, select the pencil to edit, and replace the line that reads `<!--Placeholder for Segment Snippet -->` (mine is line 5) with the Segment snippet.

Your new file should look like this:
![](https://dchtm6r471mui.cloudfront.net/notes.dropbox.com_2KqZoOTMGXjhQh7myTv8k_d.2308_1436248776313_undefined)

7.
Identify those users that submit a destination. To do so, we created a little function that captures the input from the form, and sends some of that data as trais in an identify call. While we are at it, lets also send an event using the .track method called “destination submitted.”  We are going to do that on the same index.html file, so if you haven’t committed your changes yet (if you have, just open to edit the index.html file again), scroll down to the line after the </form> (mine is line 44) and insert the following text.
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
            window.location.href = "https://www.youtube.com/watch?v=R7vmHGAshi8";
        });
        }
</script>
```
Your index.html file should contain code similar to the one found here (with your project’s Segment write key in line 7). Commit the changes. 

8.
Go back to your website and submit a travel recommendation form.
![](https://lh6.googleusercontent.com/XwmCdFqs7yF7nMYndphwPR_kyPoMVQipuUedClecnF9tjO5rh5XG77wpqa7C4znkBkBHJhN8vv2q9qSHwSewIqgTV3b-Nn0lmh8AFtAvxCYs1K2EMVKM2YwK3AmSNPUBcXQ4tvg)

Go back to your site’s debugger on the Segment’s dash. You should be able to see the following 3 calls:

![](https://dchtm6r471mui.cloudfront.net/notes.dropbox.com_2KqZoOTMGXjhQh7myTv8k_d.2308_1436278764869_undefined)

9.
Wouldnt it be nice that the page call had the actual title of the page? To make that happen, simple replace `analytics.page()` in your index.html file (mine is in line 8) with  `analytics.page(document.title)`.

your calls should now look like this:

![](https://dchtm6r471mui.cloudfront.net/notes.dropbox.com_2KqZoOTMGXjhQh7myTv8k_d.2308_1436279711665_undefined)

Congratulations! You just finished Module 1 of this training series.

One thing worth pointing out is that for simplicity purposes we didn’t follow Segment’s best practices when assigning a random userID for each user. Instead, we sent our user’s email address as the userID and that will not make Sperandio proud. The reason that sending the email is less than ideal, is because users can have many email addresses and we dont want to count one user multiple times.

What is in **Module 2**?   Notice how after submitting your form you were taken to a 404 page. That is because we redirected the user after pressing the “submit” button to the website’s blog (yourusername.github.io/blog) - but we haven’t created one yet! In module 2 we will create a blog page and a countries page using Jekyll.
We will also integrate with Optimizely and Keen. Optimizely is an interesting one, as it only integration that requires their snippet to also be loaded into our page.