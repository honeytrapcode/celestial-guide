---
layout: default
title: Celestial Guide
---

<h1>Celestial Guide</h1>
<div class="faq-container">
 {% for faq in site.faqs %}
   {% include faq-item.html faq=faq %}
 {% endfor %}
</div>

<script>
  const faqItems = document.querySelectorAll('.faq-item');
  faqItems.forEach(item => {
    item.addEventListener('click', () => {
      item.classList.toggle('active');
    });
  });
</script>
