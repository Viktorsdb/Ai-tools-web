<template>
  <div id="app">
    <header>
      <h1>AI工具站</h1>
      <input type="text" v-model="searchQuery" placeholder="搜索AI工具" @input="searchTools" />
    </header>
    <main>
      <section v-for="category in categorizedTools" :key="category.name">
        <h2>{{ category.name }}</h2>
        <ul>
          <li v-for="tool in category.tools" :key="tool.id">
            <h3>{{ tool.name }}</h3>
            <p>{{ tool.description }}</p>
            <a :href="tool.link" target="_blank">访问工具</a>
          </li>
        </ul>
      </section>
    </main>
  </div>
</template>

<script>
export default {
  data() {
    return {
      searchQuery: "",
      tools: [
        { id: 1, name: "OpenAI GPT", description: "生成文本的AI工具", category: "文本生成", link: "https://openai.com" },
        { id: 2, name: "Runway ML", description: "视频编辑和生成", category: "图像与视频", link: "https://runwayml.com" },
        { id: 3, name: "DeepL", description: "高质量翻译工具", category: "翻译", link: "https://deepl.com" },
        { id: 4, name: "Coze", description: "团队协作工具", category: "生产力", link: "https://coze.io" },
        { id: 5, name: "Suno", description: "音频生成", category: "音频处理", link: "https://suno.ai" },
      ],
    };
  },
  computed: {
    categorizedTools() {
      const categories = this.tools.reduce((acc, tool) => {
        if (!acc[tool.category]) {
          acc[tool.category] = [];
        }
        acc[tool.category].push(tool);
        return acc;
      }, {});
      return Object.keys(categories).map((category) => ({
        name: category,
        tools: categories[category],
      }));
    },
  },
  methods: {
    searchTools() {
      this.tools = this.tools.filter(tool =>
        tool.name.toLowerCase().includes(this.searchQuery.toLowerCase()) ||
        tool.description.toLowerCase().includes(this.searchQuery.toLowerCase())
      );
    },
  },
};
</script>

<style>
body {
  font-family: Arial, sans-serif;
  margin: 0;
  padding: 0;
  background-color: #f9f9f9;
}
#app {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
}
header {
  text-align: center;
  margin-bottom: 20px;
}
header h1 {
  font-size: 2rem;
  margin: 0;
}
header input {
  width: 100%;
  padding: 10px;
  margin-top: 10px;
  font-size: 1rem;
}
section {
  margin-bottom: 30px;
}
h2 {
  font-size: 1.5rem;
  color: #333;
}
ul {
  list-style: none;
  padding: 0;
}
li {
  background: #fff;
  padding: 15px;
  margin-bottom: 10px;
  border: 1px solid #ddd;
  border-radius: 5px;
}
h3 {
  margin: 0 0 5px;
  font-size: 1.2rem;
}
p {
  margin: 0 0 10px;
  color: #555;
}
a {
  color: #007bff;
  text-decoration: none;
}
a:hover {
  text-decoration: underline;
}
</style>
