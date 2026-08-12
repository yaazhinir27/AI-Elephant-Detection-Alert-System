// ElephantGuard — Main JS

// ─── Firefly Particles ───────────────────────────────
(function initParticles() {
  const container = document.getElementById('particles');
  if (!container) return;

  const count = window.innerWidth < 768 ? 15 : 30;
  for (let i = 0; i < count; i++) {
    const p = document.createElement('div');
    p.className = 'particle';
    const x = Math.random() * 100;
    const y = Math.random() * 100;
    const dur = 6 + Math.random() * 8;
    const delay = Math.random() * 8;
    const tx = (Math.random() - 0.5) * 80;
    const ty = -(Math.random() * 60 + 20);

    p.style.cssText = `
      left: ${x}%;
      top: ${y}%;
      --dur: ${dur}s;
      --delay: -${delay}s;
      --tx: ${tx}px;
      --ty: ${ty}px;
    `;
    container.appendChild(p);
  }
})();

// ─── Feature Cards Animation ─────────────────────────
(function animateFeatureCards() {
  const cards = document.querySelectorAll('.feature-card');
  if (!cards.length) return;

  const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        const delay = entry.target.dataset.delay || 0;
        setTimeout(() => {
          entry.target.style.opacity = '1';
          entry.target.style.transform = 'translateY(0)';
        }, parseInt(delay));
        observer.unobserve(entry.target);
      }
    });
  }, { threshold: 0.1 });

  cards.forEach(card => {
    card.style.opacity = '0';
    card.style.transform = 'translateY(24px)';
    card.style.transition = 'opacity 0.5s ease, transform 0.5s ease';
    observer.observe(card);
  });
})();

// ─── Smooth Scroll for Anchors ───────────────────────
document.querySelectorAll('a[href^="#"]').forEach(anchor => {
  anchor.addEventListener('click', function (e) {
    const href = this.getAttribute('href');
    if (href === '#') return;
    e.preventDefault();
    const target = document.querySelector(href);
    if (target) target.scrollIntoView({ behavior: 'smooth' });
  });
});

// ─── Global: Close modals on ESC ─────────────────────
document.addEventListener('keydown', (e) => {
  if (e.key === 'Escape') {
    document.querySelectorAll('.modal-overlay').forEach(m => {
      m.classList.add('hidden');
    });
  }
});

// ─── Navbar scroll behavior ───────────────────────────
const navbar = document.querySelector('.navbar');
if (navbar) {
  window.addEventListener('scroll', () => {
    if (window.scrollY > 20) {
      navbar.style.background = 'rgba(5, 10, 4, 0.97)';
    } else {
      navbar.style.background = 'rgba(8, 13, 6, 0.92)';
    }
  });
}

// ─── Forest ambient sound hint ────────────────────────
function showToast(msg, type = 'info', duration = 3500) {
  const existing = document.querySelector('.toast-notification');
  if (existing) existing.remove();

  const toast = document.createElement('div');
  toast.className = 'toast-notification';
  const colors = { info: '#4ade80', warning: '#fbbf24', error: '#f87171', success: '#4ade80' };
  toast.style.cssText = `
    position: fixed;
    bottom: 2rem;
    right: 2rem;
    z-index: 9999;
    padding: 0.85rem 1.5rem;
    background: rgba(13, 26, 10, 0.95);
    border: 1px solid ${colors[type]};
    border-radius: 12px;
    color: ${colors[type]};
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.85rem;
    backdrop-filter: blur(12px);
    box-shadow: 0 8px 32px rgba(0,0,0,0.4);
    animation: slideUp 0.3s ease, fadeOut 0.5s ease ${(duration - 500) / 1000}s forwards;
    max-width: 320px;
  `;
  toast.textContent = msg;
  document.body.appendChild(toast);

  const style = document.createElement('style');
  style.textContent = `
    @keyframes fadeOut { to { opacity: 0; transform: translateY(20px); } }
  `;
  document.head.appendChild(style);

  setTimeout(() => toast.remove(), duration);
}

window.showToast = showToast;
