<template>
  <div class="min-h-screen flex flex-col">
    <header>
      <div>
        <Header></Header>
      </div>
    </header>
    
    <main>
      <div class="flex-1">
        <slot></slot>
      </div>
    </main>
  
    <footer>
      <div class="pt-16">
        <Footer></Footer>
      </div>
    </footer>
  </div>
</template>