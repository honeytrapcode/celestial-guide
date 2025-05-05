---
 layout: default
 title: Celestial Guide
---

<h1>Celestial Guide</h1>
<div class="faq-container">
  {% assign sorted_faqs = site.faqs | sort: "order" %}
  {% for faq in sorted_faqs %}
    <div id="{{ faq.id }}">
      {% include faq-item.html faq=faq %}
    </div>
  {% endfor %}
</div>
 
 <script>
   const questions = document.querySelectorAll('.faq-question');
 
   questions.forEach(question => {
     question.addEventListener('click', () => {
       const item = question.parentElement;
 
       // Close all other items
       document.querySelectorAll('.faq-item').forEach(faq => {
         if (faq !== item) {
           faq.classList.remove('active');
         }
       });
 
       // Toggle clicked item
       item.classList.toggle('active');
     });
   });

   // Auto-open FAQ if hash is present in URL
   document.addEventListener('DOMContentLoaded', function() {
     if (window.location.hash) {
       const id = window.location.hash.substring(1);
       const element = document.getElementById(id);
       if (element) {
         const faqItem = element.querySelector('.faq-item');
         if (faqItem) {
           faqItem.classList.add('active');
           // Scroll to the element
           element.scrollIntoView();
         }
       }
     }
   });
 </script>
