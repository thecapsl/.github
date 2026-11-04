# CAPSuLe

**Child and Adolescent Performance Science Laboratory**

We study how children and adolescents develop as performers, and we share that
research with coaches, parents, and young athletes. This organization holds the
code behind [thecapsl.org](https://thecapsl.org).

## What we're building

[`thecapsl`](https://github.com/thecapsl/thecapsl) is the lab's website. It has
three parts:

- **Public site:** who we are, our programs, the blog archive, and ways to get
  involved or donate.
- **Members' library:** a weekly edition with an article and video. Some
  editions are free samples. The rest are for subscribers.
- **Community forum:** a members-only space for discussion, moderated by our
  staff.

## How it's built

| Layer        | Choice                                                          |
| ------------ | --------------------------------------------------------------- |
| Backend      | Python 3.12+ and Django 6.1                                     |
| Database     | PostgreSQL 16+                                                  |
| Payments     | Stripe: Embedded Checkout, customer portal, and signed webhooks |
| Frontend     | Server-rendered templates with plain CSS and JavaScript         |
| Hosting      | Amazon Web Services with gunicorn and WhiteNoise                |

We keep the stack small on purpose. There's no frontend build step or extra
service to maintain. The site is one Django project backed by a PostgreSQL
database.

## How we work

- **Every pull request is checked automatically.** GitHub Actions tests each PR
  on Python 3.12, 3.13, and 3.14 against a real PostgreSQL database. It also
  checks for missing migrations and confirms that static files build.
- **Changes go through review.** Work happens on feature branches. Pull requests
  merge into `staging` first and reach `master` after that.
- **Access control is tested.** Tests cover who can see paid content, how Stripe
  events are processed, and what staff can do. We don't want a mistake in these
  areas to reach production.
- **Paid content stays private.** A locked page contains only the public
  summary. The article text and video link are never sent to a visitor who
  doesn't have access.
- **Billing state comes from Stripe.** Access changes only after a signed Stripe
  webhook or a direct check with the Stripe API. Visiting a checkout success page
  never grants access. Each Stripe event is processed only once.
- **Secrets stay out of the repository.** Configuration comes from environment
  variables. Keys and passwords are never committed.

## Get in touch

Interested in the research, in working with us, or in supporting the lab? Visit
[thecapsl.org](https://thecapsl.org).