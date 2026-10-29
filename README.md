# Maestro Documentation

Markdown source of the documentation published at **https://maestroai.company/docs/**.

## Writing a page

- One Markdown file per page. The folder sets its section: `install/`, `guides/`, `advanced/`, `reference/`.
- Each page starts with a `title` and a `description`:

  ```md
  ---
  title: Stand-by
  description: One sentence that sums up the page.
  ---
  ```

- Images go in `images/` and are linked with a relative path: `![Alt text](../images/file.png)`.
- Links to other pages use the site path: `/docs/guides/models/`.
- Callouts: `:::tip`, `:::note`, `:::caution` or `:::danger`, closed with `:::`.
