<template>
  <div class="min-h-screen bg-gradient-to-br from-slate-50 to-blue-50">
    <!-- Header test-->
    <header class="px-4 py-6 sm:px-6 lg:px-8">
      <div class="max-w-4xl mx-auto">
        <div class="text-center mb-8">
          <div
            class="inline-flex items-center justify-center w-16 h-16 bg-blue-600 rounded-2xl mb-4 shadow-lg"
          >
            <svg
              class="w-8 h-8 text-white"
              fill="none"
              stroke="currentColor"
              viewBox="0 0 24 24"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M13.828 10.172a4 4 0 00-5.656 0l-4 4a4 4 0 105.656 5.656l1.102-1.1m0 0l4-4a4 4 0 105.656-5.656L13 5.5"
              ></path>
            </svg>
          </div>
          <h1
            class="text-3xl sm:text-4xl lg:text-5xl font-bold text-gray-900 mb-3"
          >
            URL Shortener
          </h1>
          <p class="text-lg text-gray-600 max-w-md mx-auto">
            Transform long URLs into clean, shareable links in seconds
          </p>
        </div>
      </div>
    </header>

    <!-- Main Content -->
    <main class="px-4 sm:px-6 lg:px-8 pb-8">
      <div class="max-w-4xl mx-auto">
        <!-- URL Input Card -->
        <div
          class="bg-white rounded-2xl shadow-xl p-6 sm:p-8 mb-8 border border-gray-100"
        >
          <form @submit.prevent="shortenUrl" class="space-y-4">
            <div class="relative">
              <label
                for="url-input"
                class="block text-sm font-medium text-gray-700 mb-2"
              >
                Enter your URL
              </label>
              <div class="relative">
                <input
                  id="url-input"
                  v-model="longUrl"
                  type="url"
                  placeholder="https://example.com/very/long/url/that/needs/shortening"
                  class="w-full p-4 pr-32 text-lg border-2 border-gray-200 rounded-xl focus:border-blue-500 focus:ring-0 transition-colors duration-200 placeholder-gray-400"
                  :disabled="isLoading"
                />
                <button
                  type="submit"
                  :disabled="!longUrl.trim() || isLoading"
                  class="absolute right-2 top-1/2 transform -translate-y-1/2 bg-blue-600 hover:bg-blue-700 disabled:bg-gray-300 text-white px-6 py-2 rounded-lg font-semibold transition-all duration-200 focus:outline-none focus:ring-2 focus:ring-blue-500 focus:ring-offset-2 disabled:cursor-not-allowed"
                >
                  <span v-if="!isLoading">Shorten</span>
                  <div v-else class="flex items-center space-x-2">
                    <div
                      class="w-4 h-4 border-2 border-white border-t-transparent rounded-full animate-spin"
                    ></div>
                    <span>Creating...</span>
                  </div>
                </button>
              </div>
            </div>
          </form>

          <!-- Success Result -->
          <div
            v-if="shortUrl"
            class="mt-6 p-4 bg-green-50 border border-green-200 rounded-xl"
          >
            <div class="flex items-start space-x-3">
              <div class="flex-shrink-0">
                <svg
                  class="w-6 h-6 text-green-500"
                  fill="none"
                  stroke="currentColor"
                  viewBox="0 0 24 24"
                >
                  <path
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    stroke-width="2"
                    d="M5 13l4 4L19 7"
                  ></path>
                </svg>
              </div>
              <div class="flex-1 min-w-0">
                <p class="text-sm font-medium text-green-800 mb-2">
                  URL shortened successfully!
                </p>
                <div
                  class="flex flex-col sm:flex-row sm:items-center space-y-2 sm:space-y-0 sm:space-x-3"
                >
                  <div class="flex-1 min-w-0">
                    <input
                      ref="shortUrlInput"
                      :value="shortUrl"
                      readonly
                      class="w-full p-3 text-sm bg-white border border-green-300 rounded-lg font-mono text-blue-600"
                    />
                  </div>
                  <div class="flex space-x-2">
                    <button
                      @click="copyToClipboard"
                      class="flex items-center space-x-2 bg-green-600 hover:bg-green-700 text-white px-4 py-2 rounded-lg transition-colors duration-200"
                    >
                      <svg
                        v-if="!copied"
                        class="w-4 h-4"
                        fill="none"
                        stroke="currentColor"
                        viewBox="0 0 24 24"
                      >
                        <path
                          stroke-linecap="round"
                          stroke-linejoin="round"
                          stroke-width="2"
                          d="M8 16H6a2 2 0 01-2-2V6a2 2 0 012-2h8a2 2 0 012 2v2m-6 12h8a2 2 0 002-2v-8a2 2 0 00-2-2h-8a2 2 0 00-2 2v8a2 2 0 002 2z"
                        ></path>
                      </svg>
                      <svg
                        v-else
                        class="w-4 h-4"
                        fill="none"
                        stroke="currentColor"
                        viewBox="0 0 24 24"
                      >
                        <path
                          stroke-linecap="round"
                          stroke-linejoin="round"
                          stroke-width="2"
                          d="M5 13l4 4L19 7"
                        ></path>
                      </svg>
                      <span class="hidden sm:inline">{{
                        copied ? "Copied!" : "Copy"
                      }}</span>
                    </button>
                    <a
                      :href="shortUrl"
                      target="_blank"
                      class="flex items-center space-x-2 bg-blue-600 hover:bg-blue-700 text-white px-4 py-2 rounded-lg transition-colors duration-200"
                    >
                      <svg
                        class="w-4 h-4"
                        fill="none"
                        stroke="currentColor"
                        viewBox="0 0 24 24"
                      >
                        <path
                          stroke-linecap="round"
                          stroke-linejoin="round"
                          stroke-width="2"
                          d="M10 6H6a2 2 0 00-2 2v10a2 2 0 002 2h10a2 2 0 002-2v-4M14 4h6m0 0v6m0-6L10 14"
                        ></path>
                      </svg>
                      <span class="hidden sm:inline">Visit</span>
                    </a>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>

        <!-- Error State -->
        <div
          v-if="error"
          class="mt-6 p-4 bg-red-50 border border-red-200 rounded-xl"
        >
          <div class="flex items-start space-x-3">
            <svg
              class="w-6 h-6 text-red-500 flex-shrink-0"
              fill="none"
              stroke="currentColor"
              viewBox="0 0 24 24"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M12 8v4m0 4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z"
              ></path>
            </svg>
            <div>
              <p class="text-sm font-medium text-red-800">Error</p>
              <p class="text-sm text-red-700">{{ error }}</p>
            </div>
          </div>
        </div>
      </div>

      <!-- Statistics Section -->
      <div
        class="bg-white rounded-2xl shadow-xl border border-gray-100 overflow-hidden"
      >
        <div class="px-6 py-5 border-b border-gray-200">
          <div class="flex items-center justify-between">
            <h2 class="text-xl font-bold text-gray-900">Recent URLs</h2>
            <button
              @click="fetchStats"
              :disabled="isRefreshing"
              class="inline-flex items-center space-x-2 text-sm text-gray-600 hover:text-gray-900 transition-colors duration-200"
            >
              <svg
                class="w-4 h-4 transition-transform duration-200"
                :class="{ 'animate-spin': isRefreshing }"
                fill="none"
                stroke="currentColor"
                viewBox="0 0 24 24"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="M4 4v5h.582m15.356 2A8.001 8.001 0 004.582 9m0 0H9m11 11v-5h-.581m0 0a8.003 8.003 0 01-15.357-2m15.357 2H15"
                ></path>
              </svg>
              <span>Refresh</span>
            </button>
          </div>
        </div>

        <!-- Loading State -->
        <div v-if="isLoading && urls.length === 0" class="p-8 text-center">
          <div class="inline-flex items-center space-x-3 text-gray-600">
            <div
              class="w-6 h-6 border-2 border-gray-300 border-t-blue-600 rounded-full animate-spin"
            ></div>
            <span>Loading URLs...</span>
          </div>
        </div>

        <!-- Empty State -->
        <div v-else-if="urls.length === 0" class="p-8 text-center">
          <svg
            class="w-16 h-16 text-gray-300 mx-auto mb-4"
            fill="none"
            stroke="currentColor"
            viewBox="0 0 24 24"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M13.828 10.172a4 4 0 00-5.656 0l-4 4a4 4 0 105.656 5.656l1.102-1.1m0 0l4-4a4 4 0 105.656-5.656L13 5.5"
            ></path>
          </svg>
          <p class="text-gray-500 text-lg font-medium mb-2">No URLs yet</p>
          <p class="text-gray-400">Start by shortening your first URL above</p>
        </div>

        <!-- URL List Content -->
        <div v-if="urls.length > 0">
          <!-- Desktop Table View -->
          <div class="hidden md:block overflow-x-auto">
            <table class="w-full">
              <thead class="bg-gray-50">
                <tr>
                  <th
                    class="px-6 py-4 text-left text-xs font-semibold text-gray-600 uppercase tracking-wider"
                  >
                    Short URL
                  </th>
                  <th
                    class="px-6 py-4 text-left text-xs font-semibold text-gray-600 uppercase tracking-wider"
                  >
                    Original URL
                  </th>
                  <th
                    class="px-6 py-4 text-left text-xs font-semibold text-gray-600 uppercase tracking-wider"
                  >
                    Clicks
                  </th>
                  <th
                    class="px-6 py-4 text-right text-xs font-semibold text-gray-600 uppercase tracking-wider"
                  >
                    Actions
                  </th>
                </tr>
              </thead>
              <tbody class="divide-y divide-gray-200">
                <tr
                  v-for="url in urls"
                  :key="url._id"
                  class="hover:bg-gray-50 transition-colors duration-150"
                >
                  <td class="px-6 py-4">
                    <div class="flex items-center space-x-3">
                      <div class="flex-shrink-0">
                        <div class="w-2 h-2 bg-blue-500 rounded-full"></div>
                      </div>
                      <a
                        :href="`https://url-shortener-lzgh.onrender.com/${url.shortId}`"
                        target="_blank"
                        class="font-mono text-blue-600 hover:text-blue-800 transition-colors duration-200 font-medium"
                      >
                        {{ url.shortId }}
                      </a>
                    </div>
                  </td>
                  <td class="px-6 py-4">
                    <div
                      class="max-w-xs lg:max-w-md xl:max-w-lg truncate text-gray-900"
                    >
                      {{ url.longUrl }}
                    </div>
                  </td>
                  <td class="px-6 py-4">
                    <div class="flex items-center space-x-2">
                      <div
                        class="flex items-center justify-center w-8 h-8 bg-green-100 rounded-full"
                      >
                        <svg
                          class="w-4 h-4 text-green-600"
                          fill="none"
                          stroke="currentColor"
                          viewBox="0 0 24 24"
                        >
                          <path
                            stroke-linecap="round"
                            stroke-linejoin="round"
                            stroke-width="2"
                            d="M15 12a3 3 0 11-6 0 3 3 0 016 0z"
                          ></path>
                          <path
                            stroke-linecap="round"
                            stroke-linejoin="round"
                            stroke-width="2"
                            d="M2.458 12C3.732 7.943 7.523 5 12 5c4.478 0 8.268 2.943 9.542 7-1.274 4.057-5.064 7-9.542 7-4.477 0-8.268-2.943-9.542-7z"
                          ></path>
                        </svg>
                      </div>
                      <span class="font-semibold text-gray-900">{{
                        formatClicks(url.clicks)
                      }}</span>
                    </div>
                  </td>
                  <td class="px-6 py-4 text-right">
                    <button
                      @click="copyShortUrl(url.shortId)"
                      class="inline-flex items-center space-x-1 text-sm text-gray-600 hover:text-gray-900 transition-colors duration-200"
                    >
                      <svg
                        class="w-4 h-4"
                        fill="none"
                        stroke="currentColor"
                        viewBox="0 0 24 24"
                      >
                        <path
                          stroke-linecap="round"
                          stroke-linejoin="round"
                          stroke-width="2"
                          d="M8 16H6a2 2 0 01-2-2V6a2 2 0 012-2h8a2 2 0 012 2v2m-6 12h8a2 2 0 002-2v-8a2 2 0 00-2-2h-8a2 2 0 00-2 2v8a2 2 0 002 2z"
                        ></path>
                      </svg>
                      <span>Copy</span>
                    </button>
                  </td>
                </tr>
              </tbody>
            </table>
          </div>

          <!-- Mobile Card View -->
          <div class="md:hidden divide-y divide-gray-200">
            <div
              v-for="url in urls"
              :key="url._id"
              class="p-4 hover:bg-gray-50 transition-colors duration-150"
            >
              <div class="space-y-3">
                <!-- Short URL -->
                <div class="flex items-center justify-between">
                  <div class="flex items-center space-x-3">
                    <div
                      class="w-2 h-2 bg-blue-500 rounded-full flex-shrink-0"
                    ></div>
                    <a
                      :href="`http://localhost:5000/${url.shortId}`"
                      target="_blank"
                      class="font-mono text-blue-600 hover:text-blue-800 transition-colors duration-200 font-medium text-lg"
                    >
                      {{ url.shortId }}
                    </a>
                  </div>
                  <button
                    @click="copyShortUrl(url.shortId)"
                    class="p-2 text-gray-400 hover:text-gray-600 transition-colors duration-200"
                  >
                    <svg
                      class="w-5 h-5"
                      fill="none"
                      stroke="currentColor"
                      viewBox="0 0 24 24"
                    >
                      <path
                        stroke-linecap="round"
                        stroke-linejoin="round"
                        stroke-width="2"
                        d="M8 16H6a2 2 0 01-2-2V6a2 2 0 012-2h8a2 2 0 012 2v2m-6 12h8a2 2 0 002-2v-8a2 2 0 00-2-2h-8a2 2 0 00-2 2v8a2 2 0 002 2z"
                      ></path>
                    </svg>
                  </button>
                </div>

                <!-- Original URL -->
                <div class="bg-gray-50 p-3 rounded-lg">
                  <p
                    class="text-xs font-semibold text-gray-500 uppercase tracking-wide mb-1"
                  >
                    Original URL
                  </p>
                  <p class="text-sm text-gray-900 break-all leading-relaxed">
                    {{ url.longUrl }}
                  </p>
                </div>

                <!-- Clicks -->
                <div class="flex items-center justify-between">
                  <div class="flex items-center space-x-2">
                    <div
                      class="flex items-center justify-center w-8 h-8 bg-green-100 rounded-full"
                    >
                      <svg
                        class="w-4 h-4 text-green-600"
                        fill="none"
                        stroke="currentColor"
                        viewBox="0 0 24 24"
                      >
                        <path
                          stroke-linecap="round"
                          stroke-linejoin="round"
                          stroke-width="2"
                          d="M15 12a3 3 0 11-6 0 3 3 0 016 0z"
                        ></path>
                        <path
                          stroke-linecap="round"
                          stroke-linejoin="round"
                          stroke-width="2"
                          d="M2.458 12C3.732 7.943 7.523 5 12 5c4.478 0 8.268 2.943 9.542 7-1.274 4.057-5.064 7-9.542 7-4.477 0-8.268-2.943-9.542-7z"
                        ></path>
                      </svg>
                    </div>
                    <div>
                      <p class="text-sm font-semibold text-gray-900">
                        {{ formatClicks(url.clicks) }}
                      </p>
                      <p class="text-xs text-gray-500">
                        {{ url.clicks === 1 ? "click" : "clicks" }}
                      </p>
                    </div>
                  </div>
                  <a
                    :href="
                      shortUrl.includes(url.shortId)
                        ? shortUrl
                        : `http://localhost:5000/${url.shortId}`
                    "
                    target="_blank"
                    class="inline-flex items-center space-x-1 text-sm text-blue-600 hover:text-blue-800 transition-colors duration-200"
                  >
                    <span>Visit</span>
                    <svg
                      class="w-4 h-4"
                      fill="none"
                      stroke="currentColor"
                      viewBox="0 0 24 24"
                    >
                      <path
                        stroke-linecap="round"
                        stroke-linejoin="round"
                        stroke-width="2"
                        d="M10 6H6a2 2 0 00-2 2v10a2 2 0 002 2h10a2 2 0 002-2v-4M14 4h6m0 0v6m0-6L10 14"
                      ></path>
                    </svg>
                  </a>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </main>

    <!-- Toast Notification -->
    <transition
      enter-active-class="transition duration-300 ease-out"
      enter-from-class="translate-y-2 opacity-0 sm:translate-y-0 sm:translate-x-2"
      enter-to-class="translate-y-0 opacity-100 sm:translate-x-0"
      leave-active-class="transition duration-150 ease-in"
      leave-from-class="opacity-100"
      leave-to-class="opacity-0"
    >
      <div
        v-if="showToast"
        class="fixed bottom-4 right-4 bg-gray-900 text-white px-4 py-3 rounded-lg shadow-lg z-50 flex items-center space-x-2"
      >
        <svg
          class="w-5 h-5 text-green-400"
          fill="none"
          stroke="currentColor"
          viewBox="0 0 24 24"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            d="M5 13l4 4L19 7"
          ></path>
        </svg>
        <span class="font-medium">{{ toastMessage }}</span>
      </div>
    </transition>
  </div>
</template>

<script setup>
import { ref, onMounted, nextTick } from "vue";

const longUrl = ref("");
const shortUrl = ref("");
const urls = ref([]);
const isLoading = ref(false);
const isRefreshing = ref(false);
const error = ref("");
const copied = ref(false);
const showToast = ref(false);
const toastMessage = ref("");
const shortUrlInput = ref(null);

const shortenUrl = async () => {
  if (!longUrl.value.trim()) {
    showError("Please enter a valid URL");
    return;
  }

  // Basic URL validation
  try {
    new URL(longUrl.value);
  } catch {
    showError("Please enter a valid URL (include http:// or https://)");
    return;
  }

  isLoading.value = true;
  error.value = "";

  try {
    const res = await fetch("https://url-shortener-lzgh.onrender.com/shorten", {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify({ longUrl: longUrl.value }),
    });

    if (!res.ok) {
      throw new Error(`Failed to shorten URL: ${res.status}`);
    }

    const data = await res.json();
    shortUrl.value = data.shortUrl;
    longUrl.value = "";

    // Auto-focus and select the short URL for easy copying
    await nextTick();
    if (shortUrlInput.value) {
      shortUrlInput.value.select();
    }

    await fetchStats();
    showToastMessage("URL shortened successfully!");
  } catch (err) {
    showError(err.message || "Failed to shorten URL. Please try again.");
  } finally {
    isLoading.value = false;
  }
};

const fetchStats = async () => {
  isRefreshing.value = true;
  try {
    const res = await fetch("https://url-shortener-lzgh.onrender.com/stats");
    if (!res.ok) {
      throw new Error("Failed to fetch statistics");
    }
    urls.value = await res.json();
  } catch (err) {
    showError("Failed to load URL statistics");
  } finally {
    isRefreshing.value = false;
  }
};

const copyToClipboard = async () => {
  try {
    await navigator.clipboard.writeText(shortUrl.value);
    copied.value = true;
    showToastMessage("Short URL copied to clipboard!");

    setTimeout(() => {
      copied.value = false;
    }, 2000);
  } catch (err) {
    // Fallback for browsers that don't support clipboard API
    if (shortUrlInput.value) {
      shortUrlInput.value.select();
      document.execCommand("copy");
      showToastMessage("Short URL copied to clipboard!");
    }
  }
};

const copyShortUrl = async (shortId) => {
  const fullUrl = `https://url-shortener-lzgh.onrender.com/${shortId}`;
  try {
    await navigator.clipboard.writeText(fullUrl);
    showToastMessage("Short URL copied to clipboard!");
  } catch (err) {
    // Fallback method
    const textarea = document.createElement("textarea");
    textarea.value = fullUrl;
    document.body.appendChild(textarea);
    textarea.select();
    document.execCommand("copy");
    document.body.removeChild(textarea);
    showToastMessage("Short URL copied to clipboard!");
  }
};

const formatClicks = (clicks) => {
  if (clicks >= 1000000) {
    return `${(clicks / 1000000).toFixed(1)}M`;
  } else if (clicks >= 1000) {
    return `${(clicks / 1000).toFixed(1)}K`;
  }
  return clicks.toString();
};

const showError = (message) => {
  error.value = message;
  setTimeout(() => {
    error.value = "";
  }, 5000);
};

const showToastMessage = (message) => {
  toastMessage.value = message;
  showToast.value = true;
  setTimeout(() => {
    showToast.value = false;
  }, 3000);
};

onMounted(() => {
  fetchStats();
});
</script>
