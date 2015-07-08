
# test form

<form name="email" method="post">
  <label></label>
  <input type="text" name="EMAIL" value="" placeholder="Email" />
  <input type="submit" name="submit" value="submit" />
</form>
<script type="text/javascript">
  function identify(){
    var email = this["EMAIL"].value;
    analytics.identify(email, { email: email });
    return true;
  }
  document.forms["email"].onsubmit = identify;  
</script>
