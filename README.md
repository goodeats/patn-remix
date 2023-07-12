# My personal website

Hello world!

## About

### Created with [Remix Run Epic Stack](https://github.com/epicweb-dev/epic-stack/tree/main)

The Remix Run concept resonates with me as an outstanding "project generator".
I'm a firm believer in the value of using time and energy wisely. With this in
mind, I took advantage of the Epic Stack's opinionated best-practices, enabling
me to bypass the exhausting and repetitive process of setting up standard
features such as frontend, backend, database, auth, UI, deployment, testing, and
more.

The result is a full-bodied app brought to life with a single command line,
which I believe encapsulates the potential for even more dynamic and
full-featured concept building. This aids in bringing products and ideas to
market as swiftly, reliably, and scalable as possible.

### Project Goals

This project started as a simple idea - to build a digital portfolio that
showcases my skills and experiences as a web developer. With a background in
creating full-stack apps for startups in sectors ranging from computer vision
and chat bots to health tech and e-commerce, I felt the need to establish a
platform where I could share my work.

While not all my professional details can be shared here, I hope this site
provides a glimpse into my capabilities through the various links, blog posts,
and other elements that make up this portfolio.

### Project Management

There are many project management tools and I would like to try Github's own
[Projects](https://github.com/features/issues) feature.

You can find my project for this app
[here](https://github.com/users/goodeats/projects/1). I am using this to create
[Issues](https://github.com/goodeats/patn-remix/issues) right within my repo as
development tasks to demonstrate a bit of my organizational skills.

Please forgive me if I stray a bit as this is a personal project :), but also
feel free to write your own Issue(s) if you would like to suggest something to
add or fix :D

## Development

- Initial setup:

```
npm run setup
```

- Start dev server

```
npm run dev
```

[Kent C. Dodds](https://github.com/kentcdodds) who graciously built this stack
has also inserted himself as the development admin user so check
[here](https://github.com/epicweb-dev/epic-stack/blob/main/docs/getting-started.md)
for the login details (which you can change) and his kind message

## Deployment

If you choose not to deploy your app, you can simply comment out the `deploy:`
job in `.github/workflows/deploy.yml.`

### Fly.io

Troubleshooting:

- Interesting discussion
  [here](https://github.com/epicweb-dev/epic-stack/discussions/22) about why
  deploying the Epic Stack is not-so-easy after all
- Deploying on `npx create-remix ...` was hanging on the secrets updating for
  the prod app (staging appeared to get set up properly though)
- Paying close attention to this
  [part of the discussion](https://github.com/epicweb-dev/epic-stack/discussions/22#discussioncomment-5909141)

Follow closely with these steps and
[reference](https://github.com/epicweb-dev/epic-stack/blob/main/docs/deployment.md):

- 🚨 Do Not push your repo up
  [after creating the GitHub Repository](https://github.com/epicweb-dev/epic-stack/blob/main/docs/deployment.md)
- Create the two apps for prod and staging as per the deployment instructions
  - We are not using `fly launch` with epic-stack
  - Make sure to include the 4 digits appended to the app name in `fly.toml`
- Create the Fly API token and save in the REPO secrets, not `.env`
  - Instructions for
    [Creating encrypted secrets for a repository](https://docs.github.com/en/actions/security-guides/encrypted-secrets#creating-encrypted-secrets-for-a-repository)
    here
- Add a SESSION_SECRET and INTERNAL_COMMAND_TOKEN to prod and staging as per the
  deployment instructions
  - Potentially controversial since the Fly.io dev in the interesting discussion
    is suggesting `fly launch` takes care of this, but these seem specific to
    Epic Stack
    - Actually, look at this
      [conversation](https://github.com/epicweb-dev/epic-stack/discussions/22#discussioncomment-5930053)
      about the secrets and keep in mind for future epic-stack "generations"
      with Fly.io
  - These also appear to be generated from the initial build, but that could
    just be as a key value for development
    - This
      [commit](https://github.com/epicweb-dev/epic-stack/commit/550ce76939ef99ddc09be9dfed494e6535760b69)
      sets up deployment from the init script which is great if you want to
      deploy right away and it works
- Resend for emails as per the deployment instructions
- Sentry for bug-tracking as per the deployment instructions
  [link](https://sentry.io/orgredirect/settings/:orgslug/developer-settings/new-internal/)
  - Don't have to deploy Sentry to staging
- Create volumes for prod and staging as per the deployment instructions
  - Use the [right region](https://fly.io/docs/reference/regions) for you and
    update the `primary_region` in `fly.toml`
  - There will be a warning about downtime if only 1, but you can change that
    later
    - If you are redeploying then the app will be down while the new one is
      building [more here](https://fly.io/docs/reference/volumes/)
    - Kent C Dodds with a verbal explanation
      [here](https://www.loom.com/share/c16786180172416e8a98b33faa8a157b) around
      the 2:45 mark
- Attach Consul (limits writes on db)
  - More details
    [here](https://fly.io/docs/litefs/getting-started-fly/#lease-configuration)
- Finally, now you can deploy your branch 🙌
  - Perhaps try dev first to see it deploy and then merge to main to see it in
    prod

Tests seem flaky at first, but work eventually to deploy to dev??

### Deployment takeaway

There are certainly other ways to deploy an app, but I wanted to get a handle of
the "Epic Stack" way in case the learning experince would be worth the effort (I
think so)

A little frustrating that the Epic Stack was not able to deploy out of the box
as advertised and required some troubleshooting, but issues with Fly.io and
Playwright will hopefully be smoothened out and taken on with more experience
going forward 💪
