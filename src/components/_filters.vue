<script>
export default {
  filters: {
    escape: function(value) {
      if (!value) return "";

      // unescape html encoding
      let str = unescape(escape(value.toString()));

      // strip html tags
      str = str.replace(/<[^>]*>?/g, "");

      // decode html special chars (&amp; &gt; etc)
      let elem = document.createElement("textarea");
      elem.innerHTML = str;
      str = elem.value;

      return str;
    },
    truncate: function(value, limit) {
      if (value.length > limit) {
        let index = value.lastIndexOf(" ", limit - 5);
        value = value.substring(0, index) + " [...]";
      }

      return value;
    },
    upper: function(value) {
      return !value ? "" : value.toUpperCase();
    }
  }
};
</script>
