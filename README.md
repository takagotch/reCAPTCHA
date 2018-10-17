### reCAPTCHA
---

https://github.com/ambethia/recaptcha

```
gem "recaptcha"
export RECAPTCHA_SITE_KEY = 'xxxxxxxxxxxxx'
export RECAPTCHA_SECRET_KEY = 'xxxxxxxxxxxx'

```

```ruby
# app/controllers/users_controller.rb
@user = User.new(params[:user].permit(:name))
if verify_recaptcha(model: @user) && @user.save
  redirect_to @user
else
  render 'new'
end

Recaptcha.configuration.skip_verify_env.delete("test")

# config/initializers/recaptcha.rb
Recaptcha.configure do |config|
  config.site_key = 'xxxxxx'
  config.secret_key = 'xxxxxxxxxxxxx'
  # config.proxy = 'http://myproxy.com.au:8080'
end

Recaptcha.with_configuration(site_key '12345') do
end

recaptcha_tags site_key: 'xxxxxxxx'
verify_recaptcha secret_key: 'xxxxxxx'

```

```html
<%= form_for @foo do |f| %>
  <%= recaptcha_tags %>
<% end %>
  
<%= form_for @foo do |f| %>
  <%= invisible_recaptcha_tags text: 'Submit form' %>
<% end %>
  
<% form_for @foo do |f| %>
  <%= invisible_recaptcha_tags callback 'submitInvisibleRecaptchaForm', text: 'Submit form'%>
<% end %>
  
<%= form_for @foo, html: {id: 'invisible-recaptcha-form'} do |f| %>
  <button type="button" id="submit-btn">
    Submit
  </button>
  <%= invisible_recaptcha_tags ui: :invisible, callback: 'submitInvisibleRecaptchaForm' %>
<% end %>
  
```

```js
// app/assets/javascripts/application.js
var submitInvisibleRecaptchaForm = function () {
  document.getElementById("invisible-recaptcha-form").submit();
};

//app/assets/javascripts/application.js
document.getElementById('submit-btn').addEventListener('click', function(e) {
  if(isValid){
    grecaptch.execute();
  }
});
var submitInvisibleRecaptchaForm = function(){
  document.getElementById("invisible-recaptcha-form").submit();
};

```

```yml
en:
  recaptcha:
    errrors:
      verification_failed: 'Fail'
```

