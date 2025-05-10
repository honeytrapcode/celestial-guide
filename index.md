---
layout: default
title: Celestial Guide
---

<h1>✨ Celestial Guide ✨</h1>
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
    // Handle FAQ question clicks
    const questions = document.querySelectorAll('.faq-question');
    questions.forEach(question => {
      question.addEventListener('click', () => {
        toggleFaq(question.parentElement);
      });
    });
    
    // Handle special FAQ links - Fixed to properly open target FAQ
    const faqLinks = document.querySelectorAll('.faq-link');
    faqLinks.forEach(link => {
      link.addEventListener('click', function(e) {
        e.preventDefault();
        e.stopPropagation(); // Prevent event bubbling
        const targetId = this.getAttribute('data-target');
        openFaq(targetId);
      });
    });
    
    // Function to open a specific FAQ - Improved to correctly find and open the target
    function openFaq(id) {
      // Close all FAQs first
      document.querySelectorAll('.faq-item').forEach(item => {
        item.classList.remove('active');
      });
      
      // Find and open the target FAQ
      const targetWrapper = document.getElementById(id);
      if (targetWrapper) {
        const faqItem = targetWrapper.querySelector('.faq-item');
        if (faqItem) {
          faqItem.classList.add('active');
          // Scroll to it
          targetWrapper.scrollIntoView({behavior: 'smooth'});
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
    
    // Initialize - ensure links work on first page load
    document.querySelectorAll('.faq-link').forEach(link => {
      // Make links clickable even when inside inactive FAQs
      link.style.pointerEvents = 'auto';
    });
  });
</script>