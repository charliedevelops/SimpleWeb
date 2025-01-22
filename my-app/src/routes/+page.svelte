<script>
  const appScreenshot = '/screen.png';
  const downloadLink = 'https://github.com/charliedesigns/Simple-Start';
  const demoLink = 'https://www.youtube.com/watch?v=z7rgQdmPYnE';
</script>

<div class="min-h-screen flex flex-col items-center justify-center bg-gradient-to-r from-gray-900 via-gray-800 to-gray-900 text-white">

  <section class="text-center mt-16 flex flex-col items-center">
    <h2 class="text-5xl font-extrabold mb-6 ">
      Simplify boring server tasks with <span class="text-yellow-400">Simple Start!</span>
    </h2>
    <p class="text-2xl max-w-2xl">
      Simple start makes it easy for anyone to start up or stop web servers.
    </p>
    <ul class="text-left mt-4 text-xl list-disc list-inside max-w-2xl">
      <li>Easy to edit onboarding for adding server. Optional JSON configuration also available</li>
      <li>Run any command on your local website by clicking 1 button</li>
    </ul>

    <div class="w-full max-w-4xl flex justify-center mt-8 gap-4">
      <img
        src={appScreenshot}
        alt="App Screenshot"
        class="rounded-lg shadow-lg border border-gray-800 w-1/2 transform transition-transform duration-500 hover:scale-105"
      />
      <img src="/started.png" alt="App Screenshot"         class="rounded-lg shadow-lg border border-gray-800 w-1/2 transform transition-transform duration-500 hover:scale-105"
        />
      <img src="/add.png" alt="App Screenshot"         class="rounded-lg shadow-lg border border-gray-800 w-1/2 transform transition-transform duration-500 hover:scale-105"
      />
      <img src="/config.png" alt="App Screenshot"         class="rounded-lg shadow-lg border border-gray-800 w-1/2 transform transition-transform duration-500 hover:scale-105"
      />
    </div>

    <div class="flex space-x-4 mt-8">
      <a
        href={downloadLink}
        class="bg-yellow-400 text-black px-8 py-4 rounded-lg font-medium shadow-md hover:bg-yellow-300  text-xl transform  duration-500 hover:scale-105"
      >
        Download
      </a>
      <a
        href={demoLink}
        class="bg-gray-800 text-white px-8 py-4 rounded-lg font-medium shadow-md hover:bg-gray-700  text-xl transform  duration-500 hover:scale-105"
      >
        Demo
      </a>
    </div>
  </section>

  <footer class="flex items-center justify-center mt-8">
    <img src="/logo.svg" alt="Simple Start" class="w-32 h-32 animate-spin-slow" />
  </footer>

</div>

<style>


  @keyframes spin {
    from {
      transform: rotate(0deg);
    }
    to {
      transform: rotate(360deg);
    }
  }
</style>
