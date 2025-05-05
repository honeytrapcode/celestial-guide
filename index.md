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
 </script>
