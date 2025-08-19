<script>
  const GH = {
    owner: "Vey27",
    repo: "veydigital",
    branch: "main" // change if you're publishing from another branch
  };

  async function loadReadme() {
    const target = document.getElementById("readme-body");
    if (!target) return;

    // 1) Try to fetch README from the built site (works only if README.md is copied into _site)
    try {
      const local = await fetch("/README.md", { cache: "no-store" });
      if (local.ok) {
        const md = await local.text();
        target.innerHTML = marked.parse(md);
        return;
      }
    } catch (_) {}

    // 2) Fallback to raw GitHub (reliable on Pages)
    try {
      const rawUrl = `https://raw.githubusercontent.com/${GH.owner}/${GH.repo}/${GH.branch}/README.md`;
      const res = await fetch(rawUrl, { cache: "no-store" });
      if (!res.ok) throw new Error("Failed to fetch README from raw");
      const md = await res.text();
      target.innerHTML = marked.parse(md);
    } catch (e) {
      target.innerHTML = `
        <p>Could not load README. View it on
        <a class="inline" href="https://github.com/${GH.owner}/${GH.repo}" target="_blank" rel="noopener">GitHub</a>.
        </p>`;
    }
  }

  // call once DOM is ready
  document.addEventListener("DOMContentLoaded", loadReadme);
</script>
