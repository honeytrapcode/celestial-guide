---
layout: default
title: Celestial Guide
---

<h1>Celestial Guide</h1>
<div class="faq-container">
 {% assign sorted_faqs = site.faqs | sort: "order" %}
 {% for faq in sorted_faqs %}
   {% include faq-item.html faq=faq %}
 {% endfor %}
</div>

<script>
  const faqItems = document.querySelectorAll('.faq-item');
  faqItems.forEach(item => {
     item.addEventListener('pointerdown', () => {
       item.classList.toggle('active');
    }, { passive: true });
  });
</script>
