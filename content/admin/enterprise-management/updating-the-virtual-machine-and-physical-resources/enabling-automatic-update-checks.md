---
name: GitHub Actions Demo
on: [push]
jobs:
  Explore-GitHub-Actions:
    runs-on: ubuntu-latest
    steps:
      - run: echo "🎉 The job was automatically triggered by a ${{ github.event_name }} event."
      - run: echo "🐧 This job is now running on a ${{ runner.os }} server hosted by GitHub!"
      - run: echo "🔎 The name of your branch is ${{ github.ref }} and your repository is ${{ github.repository }}."
      - name: Check out repository code
        uses: actions/checkout@v2
      - run: echo "💡 The ${{ github.repository }} repository has been cloned to the runner."
      - run: echo "🖥️ The workflow is now ready to test your code on the runner."
      - name: List files in the repository
        run: |
          ls ${{ github.workspace }}
      - run: echo "🍏 This job's status is ${{ job.status }}."

title: Enabling automatic update checks
intro: 'You can enable automatic update checks so that {% data variables.product.product_location %} checks for and downloads the latest {% data variables.product.prodname_ghe_server %} release.'
redirect_from:
  - /enterprise/admin/installation/enabling-automatic-update-checks
  - /enterprise/admin/enterprise-management/enabling-automatic-update-checks
  - /admin/enterprise-management/enabling-automatic-update-checks
versions:
  enterprise-server: '*'
type: how_to
topics:
  - Enterprise
  - Upgrades
---
When an upgrade package is automatically downloaded for {% data variables.product.product_location %}, you'll receive a message letting you know you can upgrade {% data variables.product.prodname_ghe_server %}. Packages download to the `/var/lib/ghe-updates` directory on {% data variables.product.product_location %}. For more information, see "[Upgrading {% data variables.product.prodname_ghe_server %}](/enterprise/{{ currentVersion }}/admin/guides/installation/upgrading-github-enterprise-server)."

If a hotpatch is available for an upgrade, the `.hpkg` will download automatically. In the management console you can choose to install the hotpatch immediately or schedule installation for a later time. For more information, see "[Upgrading with a hotpatch](/enterprise/{{ currentVersion }}/admin/guides/installation/upgrading-github-enterprise-server#upgrading-with-a-hotpatch)."

{% tip %}

**Tip:** To enable automatic update checks, {% data variables.product.product_location %} must be able to connect to `https://github-enterprise.s3.amazonaws.com`.

{% endtip %}

{% data reusables.enterprise_site_admin_settings.access-settings %}
{% data reusables.enterprise_site_admin_settings.management-console %}
{% data reusables.enterprise_management_console.updates-tab %}
4. Click **Yes, automatically check for updates**.
![Button for enabling automatic updates](/assets/images/enterprise/management-console/enable_updates_button.png)
{% data reusables.enterprise_management_console.save-settings %}

To see if your instance is up-to-date, check the banner on the Updates tab.

![Banner indicating your release of GitHub Enterprise Server](/assets/images/enterprise/management-console/up-to-date-banner.png)

Under **Logs**, you can see the status of the most recent update check.

![Logs for update](/assets/images/enterprise/management-console/update-log.png)
