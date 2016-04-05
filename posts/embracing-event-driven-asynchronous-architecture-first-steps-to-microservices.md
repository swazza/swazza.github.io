---
layout: default
---

## Events & Stuff

<svg id="svg" style="width:800px;height:800px"></svg>
<script>
    $(function() {
        var s = Snap("#svg");
        var rect = s.rect(10, 15, 50, 50);
        rect.attr({fill: "white"})

        var text = s.text(10, 10, "sup yo");
        text.attr({fill: "red"})
    });    
</script>
