<script setup>
import { ref, computed, onMounted } from 'vue'
import { projects, skills, certifications, experiences, t } from './content.js'

const lang = ref('fr')
const navOpen = ref(false)
const L = computed(() => t[lang.value])
function toggleLang() {
  lang.value = lang.value === 'fr' ? 'en' : 'fr'
}

const year = new Date().getFullYear()
const revealed = ref(false)
onMounted(() => requestAnimationFrame(() => (revealed.value = true)))
</script>

<template>
  <div class="page" :class="{ 'is-revealed': revealed }">
    <nav class="nav">
      <div class="wrap nav-inner">
        <a href="#top" class="nav-brand">Hana Rtibi</a>
        <button class="nav-toggle" @click="navOpen = !navOpen" aria-label="Menu">
          <span></span><span></span>
        </button>
        <div class="nav-links" :class="{ open: navOpen }">
          <a href="#experience" @click="navOpen = false">{{ L.navExperience }}</a>
          <a href="#projects" @click="navOpen = false">{{ L.navProjects }}</a>
          <a href="#skills" @click="navOpen = false">{{ L.navSkills }}</a>
          <a href="#about" @click="navOpen = false">{{ L.navAbout }}</a>
          <a href="#contact" @click="navOpen = false">{{ L.navContact }}</a>
          <button class="lang-switch" @click="toggleLang">
            {{ lang === 'fr' ? 'EN' : 'FR' }}
          </button>
        </div>
      </div>
    </nav>

    <header id="top" class="hero">
      <div class="wrap hero-inner">
        <div class="hero-avatar">
          <img src="/photo.jpg" alt="Hana Rtibi" class="avatar-img" onerror="this.style.display='none'; this.nextElementSibling.style.display='flex';" />
          <div class="avatar-fallback">HR</div>
        </div>

        <p class="hero-greeting">{{ L.greeting }}</p>
        <h1 class="hero-title">Hana Rtibi</h1>
        <p class="hero-role">{{ L.role }}</p>

        <div class="hero-status">
          <span class="dot live"></span>
          <span class="status-text">{{ L.status }}</span>
        </div>

        <p class="hero-lead">{{ L.heroLead }}</p>

        <div class="hero-actions">
          <a href="#projects" class="btn btn-primary">{{ L.viewProjects }}</a>
          <a href="#contact" class="btn btn-ghost">{{ L.contactMe }}</a>
        </div>

        <div class="cv-row">
          <a href="/cv-fr.pdf" target="_blank" class="cv-link">{{ L.cvFr }} ↓</a>
          <a href="/cv-en.pdf" target="_blank" class="cv-link">{{ L.cvEn }} ↓</a>
        </div>

        <div class="badge-row">
          <span class="badge"><span class="dot deployed"></span>AWS Certified</span>
          <span class="badge"><span class="dot deployed"></span>Spring Boot</span>
          <span class="badge"><span class="dot deployed"></span>Vue.js</span>
        </div>
      </div>
    </header>

    <section id="experience">
      <div class="wrap">
        <p class="eyebrow">{{ L.experienceEyebrow }}</p>
        <h2 class="section-title">{{ L.experienceTitle }}</h2>

        <div class="exp-list">
          <div v-for="e in experiences" :key="e.key" class="exp-item">
            <div class="exp-date">{{ e.date[lang] }}</div>
            <div class="exp-content">
              <h3 class="exp-role">{{ e.role[lang] }}</h3>
              <p class="exp-place">{{ e.place[lang] }}</p>
              <p class="exp-desc">{{ e.description[lang] }}</p>
            </div>
          </div>
        </div>
      </div>
    </section>

    <section id="projects">
      <div class="wrap">
        <p class="eyebrow">{{ L.projectsEyebrow }}</p>
        <h2 class="section-title">{{ L.projectsTitle }}</h2>

        <div class="project-grid">
          <article v-for="p in projects" :key="p.key" class="project-card" :class="{ featured: p.featured }">
            <span v-if="p.featured" class="featured-badge">★ {{ L.featuredLabel }}</span>
            <div class="project-top">
              <span class="dot" :class="p.status"></span>
              <span class="status-text">{{ p.date[lang] }}</span>
            </div>

            <h3 class="project-name">{{ p.name }}</h3>
            <p class="project-subtitle">{{ p.subtitle[lang] }}</p>
            <p class="project-desc">{{ p.description[lang] }}</p>

            <div class="stack-row">
              <span v-for="s in p.stack" :key="s" class="stack-tag">{{ s }}</span>
            </div>

            <div class="project-links" v-if="p.repo || p.demo">
              <a v-if="p.repo" :href="p.repo" target="_blank" rel="noopener" class="project-link">{{ L.repoLink }}</a>
              <a v-if="p.demo" :href="p.demo" target="_blank" rel="noopener" class="project-link">{{ L.demoLink }}</a>
            </div>
          </article>
        </div>
      </div>
    </section>

    <section id="skills">
      <div class="wrap">
        <p class="eyebrow">{{ L.skillsEyebrow }}</p>
        <h2 class="section-title">{{ L.skillsTitle }}</h2>

        <div class="skills-grid">
          <div v-for="g in skills" :key="g.group.fr" class="skills-col">
            <p class="skills-col-title">{{ g.group[lang] }}</p>
            <ul class="skills-list">
              <li v-for="s in g.items" :key="s"><span class="dot deployed"></span>{{ s }}</li>
            </ul>
          </div>
        </div>
      </div>
    </section>

    <section id="about">
      <div class="wrap">
        <p class="eyebrow">{{ L.aboutEyebrow }}</p>
        <h2 class="section-title">{{ L.aboutTitle }}</h2>
        <p class="about-text">{{ L.aboutText }}</p>

        <p class="certs-title">{{ L.certsTitle }}</p>
        <ul class="certs-list">
          <li v-for="c in certifications" :key="c.name.fr || c.name">
            <span class="dot deployed"></span>
            <span>{{ typeof c.name === 'string' ? c.name : c.name[lang] }}</span>
            <span class="status-text">{{ c.date[lang] }}</span>
          </li>
        </ul>
      </div>
    </section>

    <footer id="contact" class="contact">
      <div class="wrap contact-inner">
        <div>
          <p class="eyebrow">{{ L.contactEyebrow }}</p>
          <h2 class="section-title" style="margin-bottom: 16px;">{{ L.contactTitle }}</h2>
          <p class="about-text" style="margin-bottom: 32px;">{{ L.contactText }}</p>
        </div>
        <div class="contact-links">
          <a href="mailto:rtibihana70@gmail.com" class="contact-link">rtibihana70@gmail.com ↗</a>
          <a href="mailto:hana.rtibi@enicar.ucar.tn" class="contact-link">hana.rtibi@enicar.ucar.tn ↗</a>
          <a href="tel:+21623427432" class="contact-link">+216 23 427 432</a>
          <span class="contact-link contact-static">Tunis, Tunisie</span>
          <a href="https://www.linkedin.com/in/hana-rtibi" target="_blank" rel="noopener" class="contact-link">LinkedIn ↗</a>
          <a href="https://github.com/RtibiHana" target="_blank" rel="noopener" class="contact-link">GitHub ↗</a>
        </div>
      </div>
      <div class="wrap">
        <p class="footer-note">© {{ year }} Hana Rtibi — {{ L.footerNote }}.</p>
      </div>
    </footer>
  </div>
</template>

<style scoped>
.page { opacity: 0; transition: opacity 0.25s ease; }
.page.is-revealed { opacity: 1; }

/* nav */
.nav {
  position: sticky; top: 0; z-index: 20;
  background: rgba(246, 247, 249, 0.85);
  backdrop-filter: blur(10px);
  border-bottom: 1px solid var(--border-soft);
}
.nav-inner { display: flex; align-items: center; justify-content: space-between; height: 72px; }
.nav-brand { font-family: var(--font-display); font-weight: 700; font-size: 19px; }
.nav-links { display: flex; align-items: center; gap: 30px; font-size: 16.5px; font-weight: 500; color: var(--text-dim); }
.nav-links a { transition: color 0.15s ease; }
.nav-links a:hover { color: var(--accent); }
.lang-switch {
  font-family: var(--font-mono); font-size: 13.5px; font-weight: 700;
  background: var(--surface-alt); border: 1px solid var(--border); color: var(--text);
  padding: 9px 20px; min-width: 58px; border-radius: 20px; cursor: pointer;
}
.lang-switch:hover { border-color: var(--accent); color: var(--accent); }
.nav-toggle { display: none; flex-direction: column; gap: 5px; background: none; border: none; cursor: pointer; padding: 8px; }
.nav-toggle span { width: 20px; height: 1.5px; background: var(--text); }

/* hero — dégradé bleu ciel vers blanc */
.hero {
  padding: 40px 0 76px;
  background: linear-gradient(180deg, #bfe6fb 0%, #d9f0fc 22%, #eef8fd 48%, var(--bg) 85%);
  margin-top: -1px;
}
.hero-inner {
  display: flex; flex-direction: column; align-items: center; text-align: center;
}
.hero-avatar {
  width: 200px; height: 200px; border-radius: 50%; overflow: hidden;
  border: 3px solid #ffffff; background: var(--accent-soft);
  display: flex; align-items: center; justify-content: center;
  box-shadow: 0 14px 32px rgba(33, 138, 242, 0.18);
  margin-bottom: 20px;
}
.avatar-img { width: 100%; height: 100%; object-fit: cover; }
.avatar-fallback {
  display: none; width: 100%; height: 100%; align-items: center; justify-content: center;
  font-family: var(--font-display); font-weight: 800; font-size: 52px;
  color: var(--accent-ink); background: var(--accent-soft);
}
.hero-greeting {
  font-family: var(--font-mono); font-size: 15px; color: var(--text-dim);
  margin: 0 0 6px;
}
.hero-title {
  font-family: var(--font-display); font-size: clamp(38px, 6vw, 56px);
  line-height: 1.05; font-weight: 800; letter-spacing: -0.02em; margin: 0;
}
.hero-role { font-size: 18.5px; color: var(--accent-ink); font-weight: 600; margin: 8px 0 18px; }
.hero-status { display: flex; align-items: center; gap: 9px; margin-bottom: 26px; }
.hero-lead {
  font-size: 18px; line-height: 1.7; color: var(--text-dim);
  max-width: 540px; margin: 0 0 32px;
}
.hero-actions { display: flex; gap: 12px; margin-bottom: 22px; flex-wrap: wrap; justify-content: center; }
.btn { font-family: var(--font-mono); font-size: 14.5px; padding: 13px 24px; border-radius: var(--radius-sm); transition: all 0.15s ease; display: inline-block; }
.btn-primary { background: var(--accent); color: #fff; font-weight: 600; }
.btn-primary:hover { background: var(--accent-ink); }
.btn-ghost { border: 1px solid var(--border); color: var(--text); background: var(--surface); }
.btn-ghost:hover { border-color: var(--accent); color: var(--accent-ink); }
.cv-row { display: flex; gap: 20px; flex-wrap: wrap; justify-content: center; margin-bottom: 30px; }
.cv-link { font-family: var(--font-mono); font-size: 14px; color: var(--text-dim); border-bottom: 1px solid var(--border); }
.cv-link:hover { color: var(--accent-ink); border-color: var(--accent); }

.badge-row { display: flex; gap: 10px; flex-wrap: wrap; justify-content: center; }
.badge {
  display: flex; align-items: center; gap: 7px;
  font-family: var(--font-mono); font-size: 13px; color: var(--text-dim);
  border: 1px solid var(--border-soft); background: var(--surface);
  padding: 8px 15px; border-radius: 20px;
}

/* experience */
.exp-list { display: flex; flex-direction: column; gap: 0; }
.exp-item {
  display: grid; grid-template-columns: 140px 1fr; gap: 24px;
  padding: 22px 0; border-bottom: 1px solid var(--border-soft);
}
.exp-item:last-child { border-bottom: none; }
.exp-date { font-family: var(--font-mono); font-size: 13.5px; color: var(--text-faint); padding-top: 3px; }
.exp-role { font-family: var(--font-display); font-size: 17.5px; font-weight: 700; margin: 0 0 4px; }
.exp-place { font-size: 14px; color: var(--accent-ink); font-weight: 600; margin: 0 0 8px; }
.exp-desc { font-size: 15px; line-height: 1.6; color: var(--text-dim); margin: 0; max-width: 620px; }

/* projects */
.project-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 18px; }
.project-card {
  position: relative;
  background: var(--surface); border: 1px solid var(--border); border-radius: var(--radius);
  padding: 26px 28px; transition: border-color 0.2s ease, transform 0.2s ease, box-shadow 0.2s ease;
}
.project-card:hover { border-color: var(--accent); transform: translateY(-2px); box-shadow: 0 10px 24px rgba(20,23,31,0.06); }
.project-card.featured {
  border: 1.5px solid var(--accent);
  background: linear-gradient(180deg, var(--accent-soft) 0%, var(--surface) 90px);
}
.featured-badge {
  position: absolute; top: -11px; left: 24px;
  font-family: var(--font-mono); font-size: 11px; font-weight: 700;
  color: #fff; background: var(--accent);
  padding: 4px 12px; border-radius: 20px;
  letter-spacing: 0.02em;
}
.project-top { display: flex; align-items: center; gap: 9px; margin-bottom: 14px; }
.project-name { font-family: var(--font-display); font-size: 18px; font-weight: 700; margin: 0 0 4px; line-height: 1.3; }
.project-subtitle { font-size: 13.5px; color: var(--text-faint); margin: 0 0 12px; font-family: var(--font-mono); }
.project-desc { font-size: 15px; line-height: 1.65; color: var(--text-dim); margin: 0 0 16px; }
.stack-row { display: flex; flex-wrap: wrap; gap: 7px; margin-bottom: 16px; }
.stack-tag { font-family: var(--font-mono); font-size: 12px; color: var(--accent-ink); background: var(--accent-soft); padding: 5px 10px; border-radius: 4px; }
.project-links { display: flex; gap: 18px; }
.project-link { font-family: var(--font-mono); font-size: 13.5px; color: var(--text); border-bottom: 1px solid var(--border); }
.project-link:hover { color: var(--accent); border-color: var(--accent); }

/* skills */
.skills-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 30px 24px; }
.skills-col-title { font-family: var(--font-mono); font-size: 13px; color: var(--text-faint); text-transform: uppercase; letter-spacing: 0.06em; margin: 0 0 14px; }
.skills-list { list-style: none; padding: 0; margin: 0; display: flex; flex-direction: column; gap: 12px; }
.skills-list li { display: flex; align-items: center; gap: 10px; font-size: 15.5px; }

/* about */
.about-text { font-size: 16.5px; line-height: 1.75; color: var(--text-dim); max-width: 680px; margin: 0 0 36px; }
.certs-title { font-family: var(--font-mono); font-size: 13px; color: var(--text-faint); text-transform: uppercase; letter-spacing: 0.06em; margin: 0 0 14px; }
.certs-list { list-style: none; padding: 0; margin: 0; display: flex; flex-direction: column; gap: 12px; max-width: 560px; }
.certs-list li { display: flex; align-items: center; gap: 10px; font-size: 15.5px; }
.certs-list li span:nth-child(2) { flex: 1; }

/* contact */
.contact { padding: 84px 0 32px; }
.contact-inner { display: grid; grid-template-columns: 1.2fr 1fr; gap: 40px; margin-bottom: 40px; }
.contact-links { display: flex; flex-direction: column; gap: 2px; }
.contact-link { font-family: var(--font-mono); font-size: 15.5px; padding: 12px 0; border-bottom: 1px solid var(--border-soft); color: var(--text-dim); transition: color 0.15s ease; }
.contact-link:hover { color: var(--accent); }
.contact-static { color: var(--text-faint); cursor: default; }
.contact-static:hover { color: var(--text-faint); }
.footer-note { font-family: var(--font-mono); font-size: 13px; color: var(--text-faint); padding-top: 22px; border-top: 1px solid var(--border-soft); }

@media (max-width: 780px) {
  .nav-links {
    position: absolute; top: 72px; left: 0; right: 0; background: var(--bg);
    border-bottom: 1px solid var(--border-soft); flex-direction: column; align-items: flex-start;
    gap: 0; padding: 8px 24px 16px; display: none;
  }
  .nav-links.open { display: flex; }
  .nav-links a, .nav-links button { width: 100%; padding: 12px 0; text-align: left; border-radius: 0; }
  .nav-toggle { display: flex; }
  .exp-item { grid-template-columns: 1fr; gap: 6px; }
  .project-grid { grid-template-columns: 1fr; }
  .skills-grid { grid-template-columns: 1fr 1fr; }
  .contact-inner { grid-template-columns: 1fr; }
  section { padding: 56px 0; }
}
</style>