---
title: I nostri candidati
layout: page
---
<script src="https://cdn.jsdelivr.net/npm/@floating-ui/core@1.6.1"></script>
<script src="https://cdn.jsdelivr.net/npm/@floating-ui/dom@1.6.5"></script>
<ul class="candidati">
{% for candidato in site.data.candidati %}
  <li>
    <a href="/candidati/{{candidato.slug}}"><img src="/assets/images/{{ candidato.slug }}.jpeg" class="candidato-img"></a>
    <div class="candidato-tooltip">
      {{ candidato.name }}
      <div class="arrow"></div>
    </div>
  </li>
{% endfor %}
</ul>
<script>
const imgs = document.querySelectorAll('.candidato-img');
const tooltips = document.querySelectorAll('.candidato-tooltip');
const arrows = document.querySelectorAll('.arrow');
function update(img, tooltip, arrow) {
  window.FloatingUIDOM.computePosition(img, tooltip, {
    placement: 'top',
    middleware: [
      window.FloatingUIDOM.offset(6),
      window.FloatingUIDOM.flip(),
      window.FloatingUIDOM.shift({padding: 5}),
      window.FloatingUIDOM.arrow({element: arrow}),
    ],
  }).then(({x, y, placement, middlewareData}) => {
    Object.assign(tooltip.style, {
      left: `${x}px`,
      top: `${y + 50}px`,
    });
    const {x: arrowX, y: arrowY} = middlewareData.arrow;
    const staticSide = {
      top: 'bottom',
      right: 'left',
      bottom: 'top',
      left: 'right',
    }[placement.split('-')[0]];

    Object.assign(arrow.style, {
      left: arrowX != null ? `${arrowX}px` : '',
      top: arrowY != null ? `${arrowY}px` : '',
      right: '',
      bottom: '',
      [staticSide]: '-4px',
    });
  });
}

function showTooltip(e) {
  const tooltip = e.target.parentElement.nextElementSibling;
  const arrow = tooltip.querySelector('.arrow');
  update(e.target.parentElement, tooltip, arrow);
  tooltip.style.display = 'block';
}

function hideTooltip(e) {
  const tooltip = e.target.parentElement.nextElementSibling;
  tooltip.style.display = '';
}

[
  ['mouseenter', showTooltip],
  ['mouseleave', hideTooltip],
].forEach(([event, listener]) => {
   for (const img of imgs) img.addEventListener(event, listener);
});
</script>
