<template>
  <div class="container">
    <h1>Contact Form</h1>
    <div id="formbox">
      <form name="contact" method="POST" action="/" data-netlify="true">
        <div class="form-group">
          <label>
            お名前：
            <input type="text" name="name" />
          </label>
        </div>
        <div class="form-group">
          <label>
            メールアドレス：
            <input type="email" name="email" />
          </label>
        </div>
        <div class="form-group">
          <label>
            お問い合わせ内容：
            <textarea name="contact" rows="8"></textarea>
          </label>
        </div>
        <button type="submit" class="btn btn-primary">送信</button>
      </form>
    </div>
    
  </div>
</template>

<script>
export default {
  components: {
    
  },
  data() {
    return {
      
    }
  },
  head() {
    return {
      title: 'お問い合わせ'
    }
  }
}
</script>

<style lang="scss" scoped>
.container {
  width: 90%;
  max-width: 720px;
  margin: 30px auto;
}
h1 {
  text-align: center;
  font-size: 32px;
  font-weight: 700;
  color: #070c29;
}

input, textarea {
  display: block;
  width: 100%;
  padding: 3px 5px;
  border-radius: 5px;
  border: 1px solid #afafaf;
  font-size: 16px;
}

#formbox {
  max-width: 560px;
  margin: 20px auto;
  padding: 30px 50px;
  background: #cacde0;
}

.form-group {
  margin-bottom: 1.6rem;
  
}

.btn {
  border: none;
  border-radius: 10px;
  padding: .5rem 1.6rem;
  font-size: 18px;
  font-weight: 700;
  text-align: center;
  letter-spacing: .25em;
  &.btn-primary {
    background-color: #142066;
    color: #fff;
  }
}
</style>
