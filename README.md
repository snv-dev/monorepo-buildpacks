# Heroku Monorepo Buildpack
The purpose of this buildpack is to move and serve selected project from the root directory, rather than serving it from subfolder (because of some limitations).


# Setup

- **Required!** ** Make sure current buildpack is specified in the monorepo main `app.json` file, under the `buildpacks` section at the very beginning.
- **Required!** Make sure that `PROJECT_DIR` env variable is set in Heroku, pointing to the project directory you want to deploy. Ex. `packages/app-name`
- **Optional!** *** When creating review apps you can link the current review app with another one from the monorepo that is created by the same pull request, as you set `LINKED_APP_NAME` to the name of the other app, specified in Heroku. 

> ** In the root `app.json` file, you need to specify all buildpacks that are used across the apps.
> ```
> "buildpacks":  [
>   {
>     "url":  "https://github.com/Kosmic/monorepo-buildpack"
>   },
>   {
>     "url":  "heroku/php"
>   },
>   {
>     "url":  "heroku/nodejs"
>   }
> ]

> *** In order linked app to work, configure the review apps to use Predictable (Identifier + PR number) URL pattern! Example of linked app url will be `https://${LINKED_APP_NAME}-pr-${HEROKU_PR_NUMBER}.herokuapp.com`, where `HEROKU_PR_NUMBER` is automatically generated upon build.
> *** Make sure that in the root `app.json` file, under `env` it is set:
> ```
> "env":  {
>   "HEROKU_APP_NAME":  {
>     "required":  true
>   }
> }