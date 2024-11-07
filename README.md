
<!-- markdownlint-disable -->
# terraform-cloudinit-tor
[![pipeline status](https://gitlab.com/sr2c/terraform-cloudinit-tor/badges/main/pipeline.svg?ignore_skipped=true)](https://gitlab.com/sr2c/terraform-cloudinit-tor/-/pipelines)
[![latest release](https://gitlab.com/sr2c/terraform-cloudinit-tor/-/badges/release.svg)](https://gitlab.com/sr2c/terraform-cloudinit-tor/-/tags)
[![gitlab stars](https://img.shields.io/gitlab/stars/sr2c/terraform-cloudinit-tor)](https://gitlab.com/sr2c/terraform-cloudinit-tor/-/starrers)
<!-- markdownlint-restore -->

[![README Header][readme_header_img]][readme_header_link]

[![SR2 Communications Limited][logo]](https://www.sr2.uk/)

<!--




  ** DO NOT EDIT THIS FILE
  **
  ** This file was automatically generated by the `build-harness`.
  ** 1) Make all changes to `README.yaml`
  ** 2) Run `make init` (you only need to do this once)
  ** 3) Run`make readme` to rebuild this file.
  **
  ** (We maintain HUNDREDS of open source projects. This is how we maintain our sanity.)
  **





-->

Generates cloud-init user data for a Tor server (relay or bridge) using the latest stable Debian release. It
*may* also work with Debian derivatives but has not been tested with anything other than Debian. You may want to
check out the [sr2c/torrc](https://registry.terraform.io/modules/sr2c/torrc/) and
[sr2c/contactinfo](https://registry.terraform.io/modules/sr2c/contactinfo) modules for generating
torrc configuration files and
[ContactInfo Information Sharing Specification](https://nusenu.github.io/ContactInfo-Information-Sharing-Specification/)
lines respectively.

The tor package will be installed from the official Tor Project Debian repository at deb.torproject.org. The signing
key for the repository is included in this module.

The `obfs4proxy` and `nyx` packages can be installed by setting the respective inputs. For obfs4proxy, an apt
preference file is installed to always enable the use of stable backports. This will only work on Debian and on
other derivatives (e.g. Ubuntu) an older version of obfs4proxy would be installed from the available repositories.
Additional packages may also be installed using the `additional_packages` input.

The configuration will also change the default congestion control algorithm to BBR as it has been observed to perform
better in many of the scenarios where Tor is used. If this is really a problem then please submit an issue and it
could be made optional.

---







It's 100% Open Source and licensed under the [BSD 2-clause License](LICENSE).









## Usage


**IMPORTANT:** We do not pin modules to versions in our examples because of the
difficulty of keeping the versions in the documentation in sync with the latest released versions.
We highly recommend that in your code you pin the version to the exact version you are
using so that your infrastructure remains stable, and update versions in a
systematic way so that they do not catch you by surprise.

Also, because of a bug in the Terraform registry ([hashicorp/terraform#21417](https://github.com/hashicorp/terraform/issues/21417)),
the registry shows many of our inputs as required when in fact they are optional.
The table below correctly indicates which inputs are required.


```
module "user_data" {
  source = "sr2c/tor/cloudinit"
  # TODO: version = "x.x.x"
  torrc  = <<-EOT
  Nickname    TerraformRelay
  ORPort      9001
  ContactInfo email@example.com
  EOT
}
```






<!-- markdownlint-disable -->
## Makefile Targets
```text
Available targets:

  help                                Help screen
  help/all                            Display help for all targets
  help/short                          This help short screen
  lint                                Lint terraform code

```
<!-- markdownlint-restore -->
<!-- markdownlint-disable -->
## Requirements

| Name | Version |
|------|---------|
| <a name="requirement_terraform"></a> [terraform](#requirement\_terraform) | >= 0.15.0 |
| <a name="requirement_cloudinit"></a> [cloudinit](#requirement\_cloudinit) | >= 2.2.0 |

## Providers

| Name | Version |
|------|---------|
| <a name="provider_cloudinit"></a> [cloudinit](#provider\_cloudinit) | >= 2.2.0 |

## Modules

No modules.

## Resources

| Name | Type |
|------|------|
| [cloudinit_config.this](https://registry.terraform.io/providers/hashicorp/cloudinit/latest/docs/data-sources/config) | data source |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| <a name="input_additional_packages"></a> [additional\_packages](#input\_additional\_packages) | A list of additional packages to be installed using apt. | `list(string)` | `[]` | no |
| <a name="input_gzip"></a> [gzip](#input\_gzip) | Compress the final user-data with gzip. | `bool` | `true` | no |
| <a name="input_install_nyx"></a> [install\_nyx](#input\_install\_nyx) | Install the nyx package using apt. | `bool` | `false` | no |
| <a name="input_install_obfs4proxy"></a> [install\_obfs4proxy](#input\_install\_obfs4proxy) | Install the obfs4proxy package using apt. | `bool` | `false` | no |
| <a name="input_tailscale_auth_key"></a> [tailscale\_auth\_key](#input\_tailscale\_auth\_key) | The Tailscale auth key used to join the machine to the Tailnet. Leave as null if Tailscale should not be installed. | `string` | `null` | no |
| <a name="input_tailscale_tags"></a> [tailscale\_tags](#input\_tailscale\_tags) | A list of Tailscale tags to apply to the new server. Each tag must start with 'tag:'. | `list(string)` | `[]` | no |
| <a name="input_torrc"></a> [torrc](#input\_torrc) | The torrc configuration file to be installed. | `string` | n/a | yes |

## Outputs

| Name | Description |
|------|-------------|
| <a name="output_rendered"></a> [rendered](#output\_rendered) | The final rendered cloud-init user data. |
<!-- markdownlint-restore -->



## Share the Love

Like this project? Please give it a ★ on [our GitLab](https://gitlab.com/sr2c/terraform-cloudinit-tor)! (it helps us **a lot**)



## Related Projects

Check out these related projects.

- [terraform-null-torrc](https://gitlab.com/sr2c/terraform-null-torrc/) - Terraform module used in this module to create the torrc configuration file.
- [terraform-null-contactinfo](https://gitlab.com/sr2c/terraform-null-contactinfo/) - Terraform module that can be used to create a Tor ContactInfo-Information-Sharing-Speicifcation compliant contact info string.

## Help

**Got a question?** We got answers.

File a GitLab [issue](https://gitlab.com/sr2c/terraform-cloudinit-tor/-/issues), send us an [email][email] or join our [Matrix Community][matrix].

[![README Commercial Support][readme_commercial_support_img]][readme_commercial_support_link]

## Matrix Community

[![Matrix badge](https://img.shields.io/badge/Matrix-%23dev%3Asr2.uk-blueviolet)][matrix]

Join our [Open Source Community][matrix] on Matrix. It's **FREE** for everyone! This is the best place to talk shop, ask questions, solicit feedback, and work together as a community to build on our open source code.

## Contributing

### Bug Reports & Feature Requests

Please use the [issue tracker](https://gitlab.com/sr2c/terraform-cloudinit-tor/-/issues) to report any bugs or file feature requests.

### Developing

If you are interested in being a contributor and want to get involved in developing this project or help out with our other projects, we would love to hear from you! Shoot us an [email][email].

In general, PRs are welcome. We follow the typical "fork-and-pull" Git workflow.

 1. **Fork** the repo on GitLab
 2. **Clone** the project to your own machine
 3. **Commit** changes to your own branch
 4. **Push** your work back up to your fork
 5. Submit a **Pull Request** so that we can review your changes

**NOTE:** Be sure to merge the latest changes from "upstream" before making a pull request!


## Copyright

Copyright © 2021-2024 SR2 Communications Limited












## License

![License: BSD 2-clause](https://img.shields.io/badge/License-BSD%202--clause-blue)

```text
Redistribution and use in source and binary forms, with or without modification, are permitted provided that the
following conditions are met:

1. Redistributions of source code must retain the above copyright notice, this list of conditions and the following
   disclaimer.

2. Redistributions in binary form must reproduce the above copyright notice, this list of conditions and the following
   disclaimer in the documentation and/or other materials provided with the distribution.

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES,
INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE
DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT HOLDER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL,
SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR
SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY,
WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE
OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
```


## Trademarks

All other trademarks referenced herein are the property of their respective owners.

## About

This project is maintained by [SR2 Communications Limited][website].

[![SR2 Communications Limited][logo]][website]

We're a [DevOps services][website] company based in Aberdeen, Scotland. We ❤️ open source software and
specialise in digital human rights and humanitarian projects.

We offer [paid support][website] on all of our projects.

Check out [our other projects][gitlab], or [hire us][website] to get support with using our projects.

## Trans Rights

![Trans Rights Are Human Rights][trans_rights]

Trans is an umbrella term to describe people whose gender is not the same as, or does not sit comfortably with, the
sex they were assigned at birth. *Like all people*, they have the right to be treated with dignity and respect and to
have their human rights protected.

Trans people face significant discrimination and prejudice in many areas of their lives, including employment,
education, housing, and healthcare. They are also at increased risk of violence and hate crimes. These issues
can have a serious impact on the physical and mental well-being of trans people and can prevent them from fully
participating in society.

Trans rights are therefore an important part of the broader struggle for human rights. Everyone, regardless of
their gender identity, should be able to live their lives free from discrimination and to enjoy the same rights and
opportunities as everyone else. This includes the right to express their gender identity and to be treated with respect
and dignity.

It is important for society to recognize and respect the rights of trans people, and to take steps to address the
discrimination and prejudice that they face. This can include supporting policies and laws that protect trans
people from discrimination and promoting acceptance and understanding of trans people within the broader
community.

* [Four Pillars'](https://www.fourpillarsuk.org/) mission is to support the LGBT+ community in manners of Mental,
  Emotional, Physical & Sexual Health and offer information & support on a person-to-person basis to build a community
  that supports itself through peer education; thereby allowing individuals to make informed choices to improve their
  overall health & wellbeing.

* [Gendered Intelligence](https://genderedintelligence.co.uk/) is a trans-led and trans-involving grassroots organisation
  with a wealth of lived experience, community connections of many kinds, and a depth and breadth of trans community
  knowledge. They offer staff training, consultancy, youth work, mentoring and undertake public engagement activities.

If you have the means and you have benefited from this open source project, please consider making a donation to either
(or both) of the above groups.


## Contributors

<!-- markdownlint-disable -->
|  [![irl][irlxyz_avatar]][irlxyz_homepage]<br/>[irl][irlxyz_homepage] |
|---|
<!-- markdownlint-restore -->

  [irlxyz_homepage]: https://gitlab.com/irlxyz
  [irlxyz_avatar]: https://gitlab.com/uploads/-/system/user/avatar/5895869/avatar.png?width=130

<!-- markdownlint-disable -->
  [logo]: https://www.sr2.uk/readme/logo.png
  [website]: https://www.sr2.uk/?utm_source=gitlab&utm_medium=readme&utm_campaign=sr2c/terraform-cloudinit-tor&utm_content=website
  [gitlab]: https://go.sr2.uk/gitlab?utm_source=gitlab&utm_medium=readme&utm_campaign=sr2c/terraform-cloudinit-tor&utm_content=gitlab
  [contact]: https://go.sr2.uk/contact?utm_source=gitlab&utm_medium=readme&utm_campaign=sr2c/terraform-cloudinit-tor&utm_content=contact
  [matrix]: https://go.sr2.uk/matrix?utm_source=gitlab&utm_medium=readme&utm_campaign=sr2c/terraform-cloudinit-tor&utm_content=matrix
  [linkedin]: https://www.linkedin.com/company/sr2uk/
  [email]: mailto:contact@sr2.uk
  [readme_header_img]: https://www.sr2.uk/readme/paid-support.png
  [readme_header_link]: https://www.sr2.uk/?utm_source=gitlab&utm_medium=readme&utm_campaign=sr2c/terraform-cloudinit-tor&utm_content=readme_header_link
  [readme_commercial_support_img]: https://www.sr2.uk/readme/paid-support.png
  [readme_commercial_support_link]: https://go.sr2.uk/commerical-support?utm_source=gitlab&utm_medium=readme&utm_campaign=sr2c/terraform-cloudinit-tor&utm_content=readme_commercial_support_link
  [trans_rights]: https://img.shields.io/badge/Trans%20Rights-Human%20Rights-lightblue?logo=data:img/png;base64,iVBORw0KGgoAAAANSUhEUgAAABAAAAAQCAIAAACQkWg2AAAAGXRFWHRTb2Z0d2FyZQBBZG9iZSBJbWFnZVJlYWR5ccllPAAAADVJREFUeNpijD73i4EUwMRAIiBZA+PXlTsGm5P+//8/yJzE8m3VzkHmJNL9kKbqNMicBBBgAM3lCr5JiK9jAAAAAElFTkSuQmCC
<!-- markdownlint-restore -->
