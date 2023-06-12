---
wrapper_template: '_layouts/docs.html'
context:
  title: Migrating to Vanilla 4.0
---

# Vanilla 4.0 migration

<hr>

Vanilla 4.0 doesn’t introduce any breaking changes on SCSS code level, or in terms of removed components. It is still a major version update because it introduces new heading typography and increases the grid width. These changes may lead to visual differences and bugs.

This migration guide explains what changes are introduced in Vanilla 4.0 and how to QA them in your projects.

Vanilla 4.0 is an interim release that keeps support of old (v3) style of components, and will introduce elements of new branding and components in the new style, deprecating any unnecessary old components on the way. Some of the new components have already been added, and the reminder about them is included in this guide as well.

## Using alpha releases

Vanilla 4.0 is currently in alpha stage. This means that it is not yet ready for production use, but you can start using it in your projects to test it and report any issues you find.

Alpha versions are released to npm in `@next` tag and can be used as a dependency in your package.json:

```json
"dependencies": {
  "vanilla-framework": "{{ version }}"
}
```

You can check for the latest alpha version on [npm](https://www.npmjs.com/package/vanilla-framework?activeTab=versions) or on [GitHub](https://github.com/canonical/vanilla-framework/releases).

If you want to test out the latest unreleased version you can point your dependencies to the `vanilla-4.0` branch directly:

```json
"dependencies": {
  "vanilla-framework": "canonical/vanilla-framework#vanilla-4.0"
}
```

## Typography

Vanilla 4.0 introduces updated heading styles that are built on fewer font-sizes. We also introduce the new variable Ubuntu font.

Headings level 1 and 2 are using the same font size (2.5rem) with heading level 1 being bold. This means headings 1 are now using smaller font size than in Vanilla v3, but are bold, while headings level 2 are larger than before.

Similarly headings level 3 and 4 use the same font size (1.5rem) with level 3 being bold. Making level 3 use smaller than v3, but bold, and headings level 4 larger.

Headings level 5 and 6 don’t change. They still use the same font size as default text (1rem), with level 5 being bold, and level 6 using italics.

<div class="row--50-50">
  <div class="col"><img src="https://assets.ubuntu.com/v1/39431a6d-vanilla-4.0-migration-typography-before.png" alt="Example showing heading typography in Vanilla version 3.0"></div>
  <div class="col"><img src="https://assets.ubuntu.com/v1/dfa47513-vanilla-4.0-migration-typography-after.png" alt="Example showing new heading typography in Vanilla version 4.0"></div>
</div>

### How to update

Typography styles are built into the base styles of Vanilla and shouldn’t require any code updates. But, because this is a change that may affect the look of the website or UI make sure to QA any pages or templates that may be affected by the updated heading sizes.

If you have any custom styles or components built on top of Vanilla headings, or using Vanilla headings, also make sure that they work and look correctly.

You can search your codebase for any names listed below to find places that may be affected:

<ul class="p-list--divided" style="max-width: 40rem">
  <li class="p-list__item has-bullet">
    Elements <code>h1</code>, <code>h2</code>, <code>h3</code>, <code>h4</code>, (<code>h5</code>, <code>h6</code> if you want to be thorough)
  </li>
  <li class="p-list__item has-bullet">
    Class names: <code>p-heading--1</code>, <code>p-heading--2</code>, <code>p-heading--3</code>, <code>p-heading--4</code>, (optionally <code>p-heading--5</code>, <code>p-heading--6</code>)
  </li>
  <li class="p-list__item has-bullet">
    Placeholders <code>%vf-heading-1</code>, <code>%vf-heading-2</code>, <code>%vf-heading-3</code>, <code>%vf-heading-4</code>, (optionally <code>%vf-heading-5</code> <code>%vf-heading-6</code>)
  </li>
</ul>

## New max width of the grid

Alongside the typography changes width of the grid (max width of the page) has been adjusted as well by increasing the value of `$grid-max-width` variable from 72rem to 80rem.

### How to update

This change is automatic and doesn’t require any migration unless you have overridden the `$grid-max-width` value yourself.

Search your codebase for `$grid-max-width`:

<ul class="p-list--divided" style="max-width: 40rem">
  <li class="p-list__item has-bullet">
    If you are overriding its value, make sure you still have to. It’s best to revert to default.
  </li>
  <li class="p-list__item has-bullet">
    If you are using this variable anywhere make sure that relevant styles still work with the new value.
  </li>
</ul>

Because this change affects the look of the website, make sure you test your templates to see if there are any issues caused by width change.

Some issues that may happen include:

Images (for example in cards) that have a fixed width based on previous card size, this is especially true when using our image tag template that serves optimised images through Cloudinary.

<div class="u-fixed-width"><img src="https://assets.ubuntu.com/v1/4fbf18e2-vanilla-4.0-migration-images-width.png" alt="Example showing wrong image widths after migrating to new page max width"></div>

Old versions of global-nav have a setting for max width that may need to be adjusted.

<div class="u-fixed-width"><img src="https://assets.ubuntu.com/v1/1e8d2236-vanilla-4.0-migration-global-nav.png" alt="Example showing wrong global nav width after migrating to new page max width"></div>

Please make sure to review any templates or components that may make assumptions based on page width.

## Paper background

Vanilla 4.0 introduces a new page background used on the brochure sites. It can be applied by adding the `is-paper` class to the body element.

New pages on brochure sites should use this new background colour by default.

When using the paper background, or updating an existing page to it, make sure all content and components work well on top of the new colour.

Some issues that may be caused by paper background:
Updating old pages might require sweeping the site for images with embedded white backgrounds, and updating them to be transparent.
Components that assume white background may need to be updated.
Hover effects and active states that assume white background

To highlight sections of the page you can use a new white strip `p-strip--white`, which will create a strip with white background.

For more information see [our documentation of paper background ](/docs/base/paper), [white strip component](/docs/patterns/strip#white-strip) or [brochure layout guidelines](/docs/layouts/brochure).

## New components

Before releasing Vanilla 4.0 we started adding new components to help building brochure sites in a new style. While these are not technically new to 4.0, it’s worth taking the migration opportunity and learning more about them, and start using them where feasible.

### Section and block

Section and block components are containers that provide spacing between sections and subsections of content on brochure site pages.

In many cases new section components can replace existing strips (especially the ones that needed to have u-no-padding--top applied). Block component is used within a section.

For more information see [the section and block component documentation](/docs/patterns/section) or [brochure layout guidelines](/docs/layouts/brochure).

### Rule

New rule component provides a consistent way of adding horizontal lines that are a common element of the new style.

Use the new component in places where previously hr with u-no-margin--bottom was used.

For more information see [the rule component documentation](/docs/patterns/rule) or [brochure layout guidelines](/docs/layouts/brochure).

### Grid splits

New style of brochure sites it based on 25% (on the desktop breakpoint) splits of the grid. While such layouts can be built with our existing 12 column grid, we now also provide the most common grid splits (such as 50/50, or 25/75) that should make building the pages in a new style simpler and more consistent.

For more information see [the grid documentation](/docs/patterns/grid) or [brochure layout guidelines](/docs/layouts/brochure).

### White strip

White strip was introduced in Vanilla 4.0 as a way to highlight sections on top of a new paper background. See [“Paper background”](#paper-background) section above for more information.

<div class="p-strip">
<hr>

If you want to learn about migration to Vanilla 3.0, see [Vanilla 3.0 migration guide](/docs/migration-guide-to-v3).

</div>