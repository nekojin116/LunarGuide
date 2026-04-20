# Docusaurus Migration Notes

This file is a reminder of what will need to be changed when the guide is moved from MkDocs Material to Docusaurus.

`docs/index.md` is not expected to migrate and can be treated separately.

## Content That Will Need Changes

### 1. Replace MkDocs-only date placeholders

These pages currently use:

```md
Last updated: {{ git_revision_date_localized }}
```

That syntax is MkDocs plugin-specific and will not work in Docusaurus.

Currently found in:

- `docs/installation.md`
- `docs/updating.md`
- `docs/recommended-emulators.md`
- `docs/known-issues.md`

Possible replacement options later:

- remove the line entirely
- replace it with manual text
- use Docusaurus last update features if the target site enables them

### 2. Convert MkDocs admonitions

These blocks are MkDocs/Markdown extension syntax and will need conversion:

```md
!!! tip "Title"
    text
```

```md
!!! warning "Title"
    text
```

```md
!!! question "Title"
    text
```

```md
!!! abstract "Title"
    text
```

Docusaurus usually expects its own admonition syntax, for example:

```md
:::tip Title
text
:::
```

Currently found in:

- `docs/installation.md`

### 3. Rebuild navigation from `mkdocs.yml`

MkDocs navigation will not carry over automatically.

Current nav:

- `Home: index.md`
- `Installation: installation.md`
- `Android Build Tools: android-build-tools.md`
- `Recommended Emulators: recommended-emulators.md`
- `Known Issues: known-issues.md`
- `Updating: updating.md`
- `Tailscale Setup: tailscale-setup.md`
- `Video Resources: video.md`

This will need to be recreated in Docusaurus sidebar/navbar config.

### 4. Recreate theme settings

These MkDocs Material settings will not transfer directly:

- logo: `docs/images/icon.webp`
- favicon: `docs/images/icon.webp`
- palette settings
- `navigation.instant`
- `navigation.sections`
- `search.highlight`
- `content.code.copy`

Equivalent Docusaurus theme options will need to be configured manually.

### 5. Recreate plugin behavior

The following MkDocs plugins/extensions are currently in use and may need Docusaurus equivalents:

- `search`
- `git-revision-date-localized`
- `md_in_html`
- `attr_list`
- `admonition`
- `pymdownx.details`
- `pymdownx.superfences`

Some content may render differently in Docusaurus if these are not replaced or rewritten.

### 6. Review custom CSS

This file exists:

- `docs/stylesheets/extra.css`

It will not plug into Docusaurus automatically. Styles will need to be moved into the Docusaurus theme/custom CSS pipeline.

### 7. Move static assets

These assets will need to be copied into the new site's static/assets structure and their paths checked:

- `docs/images/*`
- `docs/fonts/*`

### 8. Check internal links and anchors

Most normal Markdown links should migrate fine, but heading anchors can differ between platforms.

These should be tested after migration:

- links like `android-build-tools.md#android-build-tools`
- links like `tailscale-setup.md#tailscale-setup`
- links like `#step-3-generate-server-code`

### 9. Review homepage assumptions

Since `docs/index.md` is not expected to migrate:

- remove it from the migrated nav/sidebar plan
- make sure any links pointing to the current homepage are updated
- decide what page should become the new landing page on the Docusaurus site

## Likely Easy To Migrate

These should mostly transfer with minimal work:

- normal Markdown headings
- paragraphs
- fenced code blocks
- most inline links
- images, after asset paths are updated

## Migration Order Recommendation

1. Copy over the Markdown pages except `docs/index.md`.
2. Replace `{{ git_revision_date_localized }}` lines.
3. Convert all `!!!` admonitions to Docusaurus admonitions.
4. Move images/fonts/CSS.
5. Rebuild sidebar and navbar config.
6. Test all internal links and anchors.
7. Fix any styling differences.

## Quick Summary

The main migration work is not rewriting the guide content itself. The main work will be:

- replacing MkDocs-specific syntax
- rebuilding site config/navigation
- moving custom styling/assets
- checking links and page rendering
