
# test form

<form role="form">
    <div class="form-group">
        <label for="email">Waitlist</label>
        <input name="email" id="email" placeholder="Email" class="form-control" type="email">
    </div>
    <div class="form-group">
        <input value="Send!" class="form-control" type="submit">
    </div>
</form>
<script type="text/javascript">
  function identify(){
    var email = this["EMAIL"].value;
    analytics.identify(email, { email: email });
    return true;
  }
  document.forms["email"].onsubmit = identify;  
</script>