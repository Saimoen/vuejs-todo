<script>
import axios from 'axios';

export default {
  mounted() {
    alert('test');

    axios.get('https://jsonplaceholder.typicode.com/todos')
      .then(response => {
        // en cas de réussite de la requête
        console.log(response);
      })
      .catch(error => {
        // en cas d’échec de la requête
        console.error(error);
      })
      .finally(() => {
        // dans tous les cas
      });
  }
}
</script>