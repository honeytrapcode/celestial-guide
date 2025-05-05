---
layout: default
title: Celestial Guide
---

<h1>Celestial Guide</h1>
<div class="faq-container">
  {% assign sorted_faqs = site.faqs | sort: "order" %}
  {% for faq in sorted_faqs %}
    <div id="{{ faq.id }}" class="faq-wrapper">
      {% include faq-item.html faq=faq %}
    </div>
  {% endfor %}
</div>

<script>
  document.addEventListener('DOMContentLoaded', function() {
    // Handle FAQ clicks
    const questions = document.querySelectorAll('.faq-question');
    
    questions.forEach(question => {
      question.addEventListener('click', () => {
        toggleFaq(question.parentElement);
      });
    });

    // Function to open a specific FAQ
    function openFaq(id) {
      // Close all FAQs first
      document.querySelectorAll('.faq-item').forEach(item => {
        item.classList.remove('active');
      });
      
      // Find and open the target FAQ
      const targetElement = document.getElementById(id);
      if (targetElement) {
        const faqItem = targetElement.querySelector('.faq-item');
        if (faqItem) {
          faqItem.classList.add('active');
          // Scroll to it
          setTimeout(() => {
            targetElement.scrollIntoView({behavior: 'smooth'});
          }, 100);
        }
      }
    }
    
    // Toggle FAQ open/closed
    function toggleFaq(item) {
      // Close all other items
      document.querySelectorAll('.faq-item').forEach(faq => {
        if (faq !== item) {
          faq.classList.remove('active');
        }
      });
      
      // Toggle clicked item
      item.classList.toggle('active');
    }

    // Check if hash is present in URL
    if (window.location.hash) {
      const id = window.location.hash.substring(1);
      openFaq(id);
    }
    
    // Add click handlers to all internal links
    document.querySelectorAll('a[href*="#"]').forEach(link => {
      link.addEventListener('click', function(e) {
        // Only handle links to the same page or base URL
        const href = this.getAttribute('href');
        if (href.includes('#')) {
          const id = href.substring(href.indexOf('#') + 1);
          if (id && document.getElementById(id)) {
            e.preventDefault();
            openFaq(id);
            // Update URL without refreshing
            history.pushState(null, null, href);
          }
        }
      });
    });
  });
</script>
