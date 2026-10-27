<?php
declare(strict_types=1);

session_start();

/* ================================================================
   1. PROFILE DATA — edit this block only
   ================================================================ */
$profile = [
    'name'     => 'Alex Morgan',
    'role'     => 'Front-End Developer & UI Engineer',
    'location' => 'Lisbon, Portugal',
    'status'   => 'Available for freelance',
    'bio'      => 'I build fast, accessible interfaces with a focus on clean design systems '
                . 'and delightful micro-interactions. Five years of experience turning '
                . 'Figma files into production-ready code that ships on time.',
    'email'    => 'alex@example.com',
    'avatar'   => 'avatar.jpg', // put a file next to this script; falls back to initials

    'skills' => [
        'HTML5', 'CSS / Sass', 'JavaScript', 'TypeScript', 'React',
        'Vue', 'Node.js', 'PHP', 'Figma', 'Accessibility', 'Git',
    ],

    'projects' => [
        [
            'title' => 'Pulse Analytics',
            'desc'  => 'Real-time dashboard with custom charts and dark mode.',
            'stack' => 'React · D3 · Tailwind',
            'url'   => 'https://example.com/pulse',
        ],
        [
            'title' => 'Orbit Commerce',
            'desc'  => 'Headless storefront with a 98 Lighthouse performance score.',
            'stack' => 'Next.js · Stripe',
            'url'   => 'https://example.com/orbit',
        ],
        [
            'title' => 'Nomad Notes',
            'desc'  => 'Offline-first note-taking PWA with local sync.',
            'stack' => 'Vue · IndexedDB',
            'url'   => 'https://example.com/nomad',
        ],
    ],

    'links' => [
        ['label' => 'Email',    'url' => 'mailto:alex@example.com',  'icon' => 'mail',     'primary' => true],
        ['label' => 'GitHub',   'url' => 'https://github.com/',       'icon' => 'github',   'primary' => false],
        ['label' => 'LinkedIn', 'url' => 'https://linkedin.com/',     'icon' => 'linkedin', 'primary' => false],
        ['label' => 'Résumé',   'url' => 'resume.pdf',                'icon' => 'download', 'primary' => false],
    ],
];

/* ================================================================
   2. HELPERS
   ================================================================ */

/** Escape any value for safe HTML output. */
function e(mixed $value): string
{
    return htmlspecialchars((string) $value, ENT_QUOTES | ENT_SUBSTITUTE, 'UTF-8');
}

/** Inline SVG icon set (no external requests). */
function icon(string $name): string
{
    $icons = [
        'mail' => '<rect x="2" y="4" width="20" height="16" rx="2"/><path d="m22 7-10 6L2 7"/>',
        'download' => '<path d="M21 15v4a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2v-4"/><path d="M7 10l5 5 5-5"/><path d="M12 15V3"/>',
    ];

    $filled = [
        'github'   => '<path d="M12 .5a12 12 0 0 0-3.8 23.4c.6.1.8-.3.8-.6v-2.1c-3.3.7-4-1.6-4-1.6-.6-1.4-1.4-1.8-1.4-1.8-1.1-.8.1-.8.1-.8 1.2.1 1.9 1.3 1.9 1.3 1.1 1.9 2.9 1.3 3.6 1 .1-.8.4-1.3.8-1.6-2.6-.3-5.4-1.3-5.4-5.9 0-1.3.5-2.4 1.2-3.2-.1-.3-.5-1.5.1-3.1 0 0 1-.3 3.3 1.2a11.4 11.4 0 0 1 6 0C17.5 4.7 18.5 5 18.5 5c.6 1.6.2 2.8.1 3.1.8.8 1.2 1.9 1.2 3.2 0 4.6-2.8 5.6-5.4 5.9.4.4.8 1.1.8 2.2v3.3c0 .3.2.7.8.6A12 12 0 0 0 12 .5Z"/>',
        'linkedin' => '<path d="M4.98 3.5a2.5 2.5 0 1 1 0 5 2.5 2.5 0 0 1 0-5ZM3 9h4v12H3V9Zm6.5 0h3.8v1.7h.1c.5-1 1.8-2 3.7-2 4 0 4.7 2.5 4.7 5.8V21h-4v-5.6c0-1.3 0-3-1.9-3s-2.2 1.4-2.2 2.9V21h-4V9Z"/>',
    ];

    if (isset($filled[$name])) {
        return '<svg viewBox="0 0 24 24" fill="currentColor" aria-hidden="true">' . $filled[$name] . '</svg>';
    }

    $path = $icons[$name] ?? $icons['mail'];

    return '<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" '
         . 'stroke-linecap="round" stroke-linejoin="round" aria-hidden="true">' . $path . '</svg>';
}

/** Increment a file-based visitor counter safely (returns 0 if not writable). */
function bump_counter(string $file): int
{
    $handle = @fopen($file, 'c+');
    if ($handle === false) {
        return 0;
    }

    flock($handle, LOCK_EX);
    $count = (int) stream_get_contents($handle) + 1;
    ftruncate($handle, 0);
    rewind($handle);
    fwrite($handle, (string) $count);
    fflush($handle);
    flock($handle, LOCK_UN);
    fclose($handle);

    return $count;
}

/* ================================================================
   3. CONTACT FORM HANDLING  (POST → validate → redirect → PRG)
   ================================================================ */

if (empty($_SESSION['csrf'])) {
    $_SESSION['csrf'] = bin2hex(random_bytes(16));
}

if ($_SERVER['REQUEST_METHOD'] === 'POST') {
    $tokenOk = isset($_POST['csrf'], $_SESSION['csrf'])
        && hash_equals($_SESSION['csrf'], (string) $_POST['csrf']);

    $old = [
        'name'    => trim((string) ($_POST['name'] ?? '')),
        'email'   => trim((string) ($_POST['email'] ?? '')),
        'message' => trim((string) ($_POST['message'] ?? '')),
    ];

    $errors = [];

    if (!$tokenOk) {
        $errors['form'] = 'Your session expired. Please try again.';
    }

    // Honeypot: real users never fill this hidden field
    if (!empty($_POST['website'])) {
        $errors['form'] = 'Spam detected.';
    }

    if (mb_strlen($old['name']) < 2 || mb_strlen($old['name']) > 60) {
        $errors['name'] = 'Please enter your name (2–60 characters).';
    }

    if (!filter_var($old['email'], FILTER_VALIDATE_EMAIL)) {
        $errors['email'] = 'Please enter a valid email address.';
    }

    $len = mb_strlen($old['message']);
    if ($len < 10 || $len > 2000) {
        $errors['message'] = 'Message must be 10–2000 characters.';
    }

    if ($errors === []) {
        $entry = sprintf(
            "[%s] %s <%s>\n%s\n---\n",
            date('Y-m-d H:i:s'),
            $old['name'],
            $old['email'],
            str_replace("\r", '', $old['message'])
        );

        @file_put_contents(__DIR__ . '/messages.log', $entry, FILE_APPEND | LOCK_EX);

        // Optional: uncomment to also send an email
        // @mail($profile['email'], 'New message from ' . $old['name'], $old['message'], 'From: ' . $old['email']);

        unset($_SESSION['csrf']);
        $_SESSION['flash'] = 'Thanks, ' . $old['name'] . '! Your message has been sent.';
        $_SESSION['old']   = [];
    } else {
        $_SESSION['errors'] = $errors;
        $_SESSION['old']    = $old;
    }

    // Post/Redirect/Get so refreshing never resubmits
    $self = strtok($_SERVER['REQUEST_URI'] ?? 'index.php', '?');
    header('Location: ' . $self . '#contact', true, 303);
    exit;
}

/* ================================================================
   4. READ SESSION STATE + THEME COOKIE
   ================================================================ */

$errors = $_SESSION['errors'] ?? [];
$old    = $_SESSION['old']    ?? ['name' => '', 'email' => '', 'message' => ''];
$flash  = $_SESSION['flash']  ?? null;
unset($_SESSION['errors'], $_SESSION['old'], $_SESSION['flash']);

$theme = $_COOKIE['theme'] ?? 'light';
if (!in_array($theme, ['light', 'dark'], true)) {
    $theme = 'light';
}

$views = bump_counter(__DIR__ . '/counter.txt');

$initials = '';
foreach (preg_split('/\s+/', trim($profile['name'])) as $part) {
    if ($part !== '') {
        $initials .= mb_strtoupper(mb_substr($part, 0, 1));
    }
}
$initials = mb_substr($initials, 0, 2);

$hasAvatar = $profile['avatar'] !== '' && is_file(__DIR__ . '/' . $profile['avatar']);
?>
<!DOCTYPE html>
<html lang="en" data-theme="<?= e($theme) ?>">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title><?= e($profile['name']) ?> — <?= e($profile['role']) ?></title>
<meta name="description" content="<?= e(mb_substr($profile['bio'], 0, 155)) ?>" />

<style>
  /* ---------- Theme tokens ---------- */
  :root {
    --bg: #f4f6fb;
    --card: #ffffff;
    --text: #1b2333;
    --muted: #6b7590;
    --accent: #6c5ce7;
    --accent-2: #00c2a8;
    --border: #e6e9f2;
    --shadow: 0 10px 30px rgba(27, 35, 51, .08);
    --radius: 18px;
    --danger: #e74c3c;
    --success: #12a87a;
  }

  [data-theme="dark"] {
    --bg: #0e1220;
    --card: #161c2e;
    --text: #eef1f8;
    --muted: #98a2bd;
    --accent: #8b7bff;
    --accent-2: #2ee6c5;
    --border: #232b42;
    --shadow: 0 10px 30px rgba(0, 0, 0, .45);
    --danger: #ff6b5b;
    --success: #2ee6a8;
  }

  /* ---------- Base ---------- */
  * { box-sizing: border-box; margin: 0; padding: 0; }

  html { scroll-behavior: smooth; }

  body {
    font-family: system-ui, -apple-system, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
    background: var(--bg);
    color: var(--text);
    line-height: 1.6;
    padding: 32px 16px 64px;
    transition: background .3s ease, color .3s ease;
    -webkit-font-smoothing: antialiased;
  }

  .wrap { max-width: 880px; margin: 0 auto; }

  /* ---------- Card ---------- */
  .profile {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: var(--radius);
    box-shadow: var(--shadow);
    overflow: hidden;
  }

  /* ---------- Header ---------- */
  .header {
    position: relative;
    padding: 84px 28px 28px;
    text-align: center;
    background:
      radial-gradient(600px 200px at 20% 0%, rgba(108, 92, 231, .28), transparent 70%),
      radial-gradient(600px 220px at 85% 10%, rgba(0, 194, 168, .22), transparent 70%),
      linear-gradient(135deg, var(--accent), var(--accent-2));
    background-blend-mode: screen;
  }

  .avatar {
    width: 132px; height: 132px;
    margin: 0 auto 16px;
    border-radius: 50%;
    border: 4px solid var(--card);
    box-shadow: 0 8px 24px rgba(0, 0, 0, .22);
    overflow: hidden;
    display: grid;
    place-items: center;
    background: linear-gradient(135deg, #ffffff, #d9e2ff);
    font-size: 42px;
    font-weight: 700;
    color: #4b3fd1;
    letter-spacing: 1px;
  }
  .avatar img { width: 100%; height: 100%; object-fit: cover; display: block; }

  .name { font-size: 1.9rem; line-height: 1.2; color: #fff; }
  .role { color: rgba(255, 255, 255, .92); font-weight: 500; margin-top: 4px; }
  .location { color: rgba(255, 255, 255, .82); font-size: .9rem; margin-top: 6px; }

  .badge {
    display: inline-flex;
    align-items: center;
    gap: 7px;
    margin-top: 14px;
    padding: 5px 14px;
    border-radius: 999px;
    font-size: .78rem;
    font-weight: 600;
    color: #fff;
    background: rgba(255, 255, 255, .18);
    border: 1px solid rgba(255, 255, 255, .4);
    backdrop-filter: blur(6px);
  }
  .badge::before {
    content: "";
    width: 7px; height: 7px;
    border-radius: 50%;
    background: #37ffb0;
    box-shadow: 0 0 0 3px rgba(55, 255, 176, .28);
  }

  /* ---------- Sections ---------- */
  .body { padding: 28px; display: grid; gap: 32px; }

  .section-title {
    font-size: .78rem;
    text-transform: uppercase;
    letter-spacing: .14em;
    color: var(--muted);
    font-weight: 700;
    margin-bottom: 12px;
  }

  .bio { color: var(--muted); max-width: 62ch; }

  /* ---------- Skills ---------- */
  .tags { display: flex; flex-wrap: wrap; gap: 8px; }
  .tag {
    font-size: .85rem;
    font-weight: 600;
    padding: 6px 14px;
    border-radius: 999px;
    color: var(--accent);
    background: color-mix(in srgb, var(--accent) 12%, transparent);
    border: 1px solid color-mix(in srgb, var(--accent) 25%, transparent);
  }

  /* ---------- Projects ---------- */
  .grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
    gap: 16px;
  }

  .project {
    display: block;
    padding: 18px;
    border: 1px solid var(--border);
    border-radius: 14px;
    text-decoration: none;
    color: inherit;
    transition: transform .2s ease, border-color .2s ease, box-shadow .2s ease;
  }
  .project:hover {
    transform: translateY(-4px);
    border-color: var(--accent);
    box-shadow: 0 12px 24px rgba(108, 92, 231, .16);
  }
  .project h3 { font-size: 1rem; margin-bottom: 6px; }
  .project p { font-size: .88rem; color: var(--muted); }
  .project .stack {
    font-size: .78rem;
    color: var(--accent-2);
    font-weight: 600;
    margin-top: 10px;
    display: block;
  }

  /* ---------- Buttons ---------- */
  .links { display: flex; flex-wrap: wrap; gap: 10px; }
  .btn {
    display: inline-flex;
    align-items: center;
    gap: 8px;
    padding: 10px 18px;
    border-radius: 12px;
    font-size: .9rem;
    font-weight: 600;
    font-family: inherit;
    text-decoration: none;
    color: var(--text);
    background: var(--bg);
    border: 1px solid var(--border);
    cursor: pointer;
    transition: background .2s ease, color .2s ease, transform .2s ease, border-color .2s ease;
  }
  .btn:hover { transform: translateY(-2px); border-color: var(--accent); color: var(--accent); }
  .btn.primary {
    background: linear-gradient(135deg, var(--accent), var(--accent-2));
    color: #fff;
    border: 0;
  }
  .btn.primary:hover { color: #fff; filter: brightness(1.07); }
  .btn svg { width: 16px; height: 16px; flex: none; }

  /* ---------- Contact form ---------- */
  .form-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 14px;
  }
  .field { display: grid; gap: 6px; }
  .field.full { grid-column: 1 / -1; }

  label {
    font-size: .82rem;
    font-weight: 600;
    color: var(--muted);
  }

  input, textarea {
    width: 100%;
    padding: 11px 14px;
    font: inherit;
    font-size: .92rem;
    color: var(--text);
    background: var(--bg);
    border: 1px solid var(--border);
    border-radius: 11px;
    transition: border-color .2s ease, box-shadow .2s ease;
  }
  input:focus, textarea:focus {
    outline: none;
    border-color: var(--accent);
    box-shadow: 0 0 0 3px color-mix(in srgb, var(--accent) 20%, transparent);
  }
  textarea { resize: vertical; min-height: 120px; }
  input.invalid, textarea.invalid { border-color: var(--danger); }

  .error-text { font-size: .78rem; color: var(--danger); font-weight: 500; }

  .honeypot {
    position: absolute;
    left: -9999px;
    width: 1px; height: 1px;
    overflow: hidden;
  }

  .alert {
    padding: 12px 16px;
    border-radius: 12px;
    font-size: .88rem;
    font-weight: 500;
    margin-bottom: 16px;
  }
  .alert.success {
    color: var(--success);
    background: color-mix(in srgb, var(--success) 12%, transparent);
    border: 1px solid color-mix(in srgb, var(--success) 30%, transparent);
  }
  .alert.error {
    color: var(--danger);
    background: color-mix(in srgb, var(--danger) 12%, transparent);
    border: 1px solid color-mix(in srgb, var(--danger) 30%, transparent);
  }

  .form-footer {
    grid-column: 1 / -1;
    display: flex;
    flex-wrap: wrap;
    align-items: center;
    justify-content: space-between;
    gap: 12px;
    margin-top: 4px;
  }
  .hint { font-size: .76rem; color: var(--muted); }

  /* ---------- Footer ---------- */
  .footer {
    text-align: center;
    padding: 18px;
    font-size: .82rem;
    color: var(--muted);
    border-top: 1px solid var(--border);
  }

  /* ---------- Theme toggle ---------- */
  .toggle {
    position: absolute;
    top: 14px; right: 14px;
    width: 42px; height: 42px;
    border-radius: 50%;
    border: 1px solid rgba(255, 255, 255, .45);
    background: rgba(255, 255, 255, .18);
    backdrop-filter: blur(6px);
    color: #fff;
    font-size: 1.1rem;
    cursor: pointer;
    display: grid;
    place-items: center;
    transition: background .2s ease;
  }
  .toggle:hover { background: rgba(255, 255, 255, .32); }

  /* ---------- Small screens ---------- */
  @media (max-width: 560px) {
    .form-grid { grid-template-columns: 1fr; }
  }
  @media (max-width: 480px) {
    .header { padding: 72px 18px 24px; }
    .body { padding: 22px 18px; }
    .name { font-size: 1.55rem; }
    .avatar { width: 108px; height: 108px; font-size: 34px; }
  }

  /* Respect reduced-motion preferences */
  @media (prefers-reduced-motion: reduce) {
    * { transition: none !important; }
    html { scroll-behavior: auto; }
  }
</style>
</head>

<body>
<div class="wrap">
  <main class="profile">

    <!-- ================= Header ================= -->
    <header class="header">
      <button class="toggle" id="themeToggle" aria-label="Toggle dark mode">
        <?= $theme === 'dark' ? '☀️' : '🌙' ?>
      </button>

      <div class="avatar">
        <?php if ($hasAvatar): ?>
          <img src="<?= e($profile['avatar']) ?>" alt="Portrait of <?= e($profile['name']) ?>" />
        <?php else: ?>
          <?= e($initials) ?>
        <?php endif; ?>
      </div>

      <h1 class="name"><?= e($profile['name']) ?></h1>
      <p class="role"><?= e($profile['role']) ?></p>
      <p class="location">📍 <?= e($profile['location']) ?></p>

      <?php if ($profile['status'] !== ''): ?>
        <p class="badge"><?= e($profile['status']) ?></p>
      <?php endif; ?>
    </header>

    <div class="body">

      <!-- ================= About ================= -->
      <section aria-labelledby="about-title">
        <h2 class="section-title" id="about-title">About</h2>
        <p class="bio"><?= e($profile['bio']) ?></p>
      </section>

      <!-- ================= Skills ================= -->
      <section aria-labelledby="skills-title">
        <h2 class="section-title" id="skills-title">Skills</h2>
        <div class="tags">
          <?php foreach ($profile['skills'] as $skill): ?>
            <span class="tag"><?= e($skill) ?></span>
          <?php endforeach; ?>
        </div>
      </section>

      <!-- ================= Projects ================= -->
      <section aria-labelledby="projects-title">
        <h2 class="section-title" id="projects-title">Selected Projects</h2>
        <div class="grid">
          <?php foreach ($profile['projects'] as $project): ?>
            <a class="project" href="<?= e($project['url']) ?>" target="_blank" rel="noopener noreferrer">
              <h3><?= e($project['title']) ?></h3>
              <p><?= e($project['desc']) ?></p>
              <span class="stack"><?= e($project['stack']) ?></span>
            </a>
          <?php endforeach; ?>
        </div>
      </section>

      <!-- ================= Links ================= -->
      <section aria-labelledby="links-title">
        <h2 class="section-title" id="links-title">Get in touch</h2>
        <div class="links">
          <?php foreach ($profile['links'] as $link): ?>
            <a class="btn<?= $link['primary'] ? ' primary' : '' ?>"
               href="<?= e($link['url']) ?>"
               <?= str_starts_with($link['url'], 'http') ? 'target="_blank" rel="noopener noreferrer"' : '' ?>>
              <?= icon($link['icon']) ?>
              <?= e($link['label']) ?>
            </a>
          <?php endforeach; ?>
        </div>
      </section>

      <!-- ================= Contact form ================= -->
      <section id="contact" aria-labelledby="contact-title">
        <h2 class="section-title" id="contact-title">Send a message</h2>

        <?php if ($flash !== null): ?>
          <div class="alert success" role="status"><?= e($flash) ?></div>
        <?php endif; ?>

        <?php if (isset($errors['form'])): ?>
          <div class="alert error" role="alert"><?= e($errors['form']) ?></div>
        <?php endif; ?>

        <form method="post" action="#contact" class="form-grid" novalidate>
          <input type="hidden" name="csrf" value="<?= e($_SESSION['csrf']) ?>" />

          <!-- Honeypot: hidden from humans, tempting to bots -->
          <div class="honeypot" aria-hidden="true">
            <label for="website">Website</label>
            <input type="text" id="website" name="website" tabindex="-1" autocomplete="off" />
          </div>

          <div class="field">
            <label for="name">Name</label>
            <input type="text" id="name" name="name" required maxlength="60"
                   value="<?= e($old['name']) ?>"
                   class="<?= isset($errors['name']) ? 'invalid' : '' ?>"
                   aria-describedby="<?= isset($errors['name']) ? 'err-name' : '' ?>" />
            <?php if (isset($errors['name'])): ?>
              <span class="error-text" id="err-name"><?= e($errors['name']) ?></span>
            <?php endif; ?>
          </div>

          <div class="field">
            <label for="email">Email</label>
            <input type="email" id="email" name="email" required maxlength="120"
                   value="<?= e($old['email']) ?>"
                   class="<?= isset($errors['email']) ? 'invalid' : '' ?>"
                   aria-describedby="<?= isset($errors['email']) ? 'err-email' : '' ?>" />
            <?php if (isset($errors['email'])): ?>
              <span class="error-text" id="err-email"><?= e($errors['email']) ?></span>
            <?php endif; ?>
          </div>

          <div class="field full">
            <label for="message">Message</label>
            <textarea id="message" name="message" required minlength="10" maxlength="2000"
                      class="<?= isset($errors['message']) ? 'invalid' : '' ?>"
                      aria-describedby="<?= isset($errors['message']) ? 'err-message' : '' ?>"><?= e($old['message']) ?></textarea>
            <?php if (isset($errors['message'])): ?>
              <span class="error-text" id="err-message"><?= e($errors['message']) ?></span>
            <?php endif; ?>
          </div>

          <div class="form-footer">
            <button class="btn primary" type="submit">
              <?= icon('mail') ?>
              Send message
            </button>
            <span class="hint">Your details are never shared.</span>
          </div>
        </form>
      </section>

    </div>

    <footer class="footer">
      © <?= date('Y') ?> <?= e($profile['name']) ?> — Built with PHP.
      <?php if ($views > 0): ?>
        · <?= number_format($views) ?> profile view<?= $views === 1 ? '' : 's' ?>
      <?php endif; ?>
    </footer>
  </main>
</div>

<script>
  // Theme toggle — persisted in a cookie so PHP can render the right theme on load
  (function () {
    const root = document.documentElement;
    const toggle = document.getElementById('themeToggle');

    toggle.addEventListener('click', () => {
      const next = root.getAttribute('data-theme') === 'dark' ? 'light' : 'dark';
      root.setAttribute('data-theme', next);
      toggle.textContent = next === 'dark' ? '☀️' : '🌙';
      document.cookie = 'theme=' + next + ';path=/;max-age=31536000;samesite=lax';
    });
  })();

  // Client-side nicety: keep focus on the first invalid field after a failed submit
  (function () {
    const firstInvalid = document.querySelector('.invalid');
    if (firstInvalid && location.hash === '#contact') {
      firstInvalid.focus({ preventScroll: false });
    }
  })();
</script>
</body>
</html>
