
# Module 1. Implementing Segment
Build a single page website and implement Segment from scratch in 5 steps. Completion time 45 minutes

## 1. Create an Account
Create an account in GitHub (https://github.com/new) or sign in.

## 2. Create a Repo
Create a new repository (click on the black + sign on the top right) and call it `yourusername.github.io` . In my case, my new repository is called `beckyjaimes.github.io`, check the box that initializes the repo with a README file, and click on the “Create repository” button.
![](https://cloudup.com/ch3rFGk5D3P+)

## 3. Create an index.html file
Create a new file by clicking on the blue + symbol next to your new repository’s name and call it index.html (this file will contain the code for your website’s default page)

![](https://cloudup.com/c0cFaR-2xwe+)

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

On a separate window, navigate to  yourusername.github.io. There you should be able to see your new website (it might take up to 5 minutes). Should look similar to this:

![](https://cloudup.com/c7XrmvISWfJ+)

## 4. Implement Segment 
Create a Segment project and click on the “install a library in your site or mobile app” option (or select it by clicking on the 6th icon called “setup project”)

![](https://cloudup.com/co7DtWt5aOO+)

Copy the full snippet from the box on your segment dashboard, go back to your `index.html` file, select the pencil to edit, and replace the line that reads `<!--Placeholder for Segment Snippet -->` (mine is line 8) with the Segment snippet.

Your new file should look like this:
![](https://cloudup.com/ckTqBYoDp7L+)

## 5. Identify Users and Track an Event
Identify those users that submit a destination. To do so, we created a little function that captures the input from the form, and sends some of that data as trais in an identify call. While we are at it, lets also send an event using the .track method called “destination submitted.”  We are going to do that on the same index.html file, so if you haven’t committed your changes yet (if you have, just open to edit the index.html file again), scroll down to the line after the </form> (mine is line 38) and insert the following text.
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
            window.location.href = "";
        });
        }
</script>
```
Your index.html file should contain code similar to the one found [here](https://gist.github.com/TheBecky/76eaa40b43a82a900c82) (with your project’s Segment write key in line 10). Commit the changes. 

Go back to your website (refresh to make sure all changes have been loaded) and submit a travel recommendation form.
![](https://cloudup.com/cdWxA9BwOdr+)

Go to your debugger on the Segment’s dash. You should be able to see the following 3 calls:

![](https://cloudup.com/c245KeijI5E+)

## 6. Bonus Step
Wouldnt it be nice that the page call had the actual title of the page? To do that, you just have to replace `analytics.page()` in your index.html file (mine is in line 11) with  `analytics.page(document.title)`.

your calls should now look like this:

![](https://cloudup.com/cbaLOR5Jjjb+)

Congratulations! You just finished Module 1 of this training series.

One thing worth pointing out is that for simplicity purposes we didn’t follow Segment’s best practices when assigning a random userID for each user. Instead, we sent our user’s email address as the userID and that will not make Sperandio proud. The reason that sending the email is less than ideal, is because users can have many email addresses and we dont want to count one user multiple times.

In module 2 we will  integrate with Optimizely and Keen. Optimizely is an interesting one, as it only integration that requires their snippet to also be loaded into our page.