OmniAuth with Devise already installed and configured


- add 'omniauth-<provider>' to Gemfile
(it will depend on OmniAuth so no need to add it explicitely)
- BUNDLE
- modify config/initializers/devise.rb
to activate wanted provider (search for 'omniauth' in this file!)
- create an app token at wanted provider's dev section (developper.facebook.com for instance)
=> get the appID and secretToken to modify devise.omniauth config accordingly
- modify User model for it to be :omniauthable
(no need to modify DB schema for now)

- restart your server

Devise authentication forms should now have a 
link to login with your wanted provider

Authenticating with provider should be ok but redirecting to an error on your app:
Devise/OmniAuth doesn't know where to go when provider has given authentication informations:

- Modify routes.rb to add the omniauth callbacks controller

  devise_for :users, :controllers => { :omniauth_callbacks => "omniauth_callbacks" }

- Create the omniauthcontroller (derivated from Devise's controller)

  class OmniauthCallbacksController < Devise::OmniauthCallbacksController
  end




callbacks have the form (CF %APP/rails/info/routes)


Good example: GitHub
by default it won't give you the user's email: perfect to test uncomplete provider sign-in !

Create GH app (for tokens) here:
https://github.com/settings/applications


