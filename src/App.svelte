<script>
  import "@fortawesome/fontawesome-free/css/all.css";
  import "./assets/global.css";
  import Home from "./pages/Home.svelte";
  import Book from "./pages/Book.svelte";
  import NotFound from "./pages/NotFound.svelte";
  import Books from "./pages/Books.svelte";
  import AddItem from "./pages/AddItem.svelte";
  import AddItemBookSelect from "./pages/AddItemBookSelect.svelte";
  import AddBook from "./pages/AddBook.svelte";
  import EditBook from "./pages/EditBook.svelte";
  import EditWordSelect from "./pages/EditWordSelect.svelte";
  import EditWord from "./pages/EditWord.svelte";
  import { v4 as uuidv4 } from "uuid";
  import SuccessToast from "./components/SuccessToast.svelte";
  import ErrorToast from "./components/ErrorToast.svelte";
  let successMessageText = "";
  let successMessageOpen = false;
  let errorMessageText = "";
  let errorMessageOpen = false;
  let notebooks = [];
  if (localStorage.getItem("chineseoo-notes") != null) {
    notebooks = JSON.parse(localStorage.getItem("chineseoo-notes"));
  }
  // notebooks = [
  //   {
  //     name: "成語",
  //     type: "idiom",
  //     id: "1",
  //     data: [
  //       {
  //         text: "覆水難收",
  //         id:
  //         description: "已經潑出去的水很難收回。比喻離異的夫妻很難再復合。"
  //       }
  //     ]
  //   },
  //   {
  //     name: "字詞",
  //     type: "word",
  //     id: "2",
  //     data: [
  //       {
  //         text: "權力",
  //         description: "指法律所賦予人民的私權"
  //       }
  //     ]
  //   }
  // ]
  const routingMap = {
    "#/": Home,
    ":book": Book,
    "#/book/": Books,
    ":additem": AddItem,
    "#/additem/": AddItemBookSelect,
    "#/addbook/": AddBook,
    "#/editbook/": EditBook,
    ":editword": EditWord,
    "#/editword/": EditWordSelect,
  };
  const beautify_hash = (text) => {
    let arr = text.split("/");
    if (arr[arr.length - 1] != "") {
      arr.push("");
    }
    text = arr.join("/");
    return text;
  };
  const redirect_hash = (from, to) => {
    from = beautify_hash(from);
    to = beautify_hash(to);
    let hash = beautify_hash(location.hash);
    if (hash == from) {
      location.hash = to;
    }
  };
  let page;
  let hashParam;
  const routeChange = () => {
    redirect_hash("", "#/");
    if (location.hash.split("/")[1] == "book") {
      if (location.hash.split("/")[2]) {
        hashParam = location.hash.split("/")[2];
        page = routingMap[":" + location.hash.split("/")[1]] || NotFound;
      } else {
        hashParam = "";
        page = routingMap["#/book/"] || NotFound;
      }
    } else if (location.hash.split("/")[1] == "additem") {
      if (location.hash.split("/")[2]) {
        hashParam = location.hash.split("/")[2];
        page = routingMap[":" + location.hash.split("/")[1]] || NotFound;
      } else {
        hashParam = "";
        page = routingMap["#/additem/"] || NotFound;
      }
    } else if (location.hash.split("/")[1] == "editword") {
      if (location.hash.split("/")[2]) {
        hashParam = location.hash.split("/")[2];
        page = routingMap[":" + location.hash.split("/")[1]] || NotFound;
      } else {
        hashParam = "";
        page = routingMap["#/editword/"] || NotFound;
      }
    } else {
      let hash = beautify_hash(location.hash);
      console.log(hash);
      page = routingMap[location.hash] || NotFound;
    }
  };
  const add_new_book = (e) => {
    console.log(e.detail);
    let id = uuidv4();
    notebooks.push({
      name: e.detail.name_input,
      type: "idiom",
      id,
      data: [],
    });
    try {
      localStorage.setItem("chineseoo-notes", JSON.stringify(notebooks));
    } catch (e) {
      if (e == QUOTA_EXCEEDED_ERR) {
        errorMessageText = "Local Storage Quota exceeded!";
        errorMessageOpen = true;
        setTimeout(() => {
          errorMessageOpen = false;
        }, 1000);
        return;
      }
    }
    successMessageText = "Added Book " + e.detail.name_input;
    successMessageOpen = true;
    setTimeout(() => {
      successMessageOpen = false;
    }, 1000);
  };
  const add_new_word = (e) => {
    console.log(e.detail);
    let id = uuidv4();
    let bookIndex = notebooks.findIndex((book) => {
      console.log(book.id, e.detail.hashParam);
      return book.id == e.detail.hashParam;
    });
    console.log(bookIndex);
    notebooks[bookIndex].data.push({
      text: e.detail.name_input,
      type: "text",
      description: e.detail.content_input,
      id,
    });
    try {
      localStorage.setItem("chineseoo-notes", JSON.stringify(notebooks));
    } catch (e) {
      if (e == QUOTA_EXCEEDED_ERR) {
        errorMessageText = "Local Storage Quota exceeded!";
        errorMessageOpen = true;
        setTimeout(() => {
          errorMessageOpen = false;
        }, 1000);
        return;
      }
    }
    successMessageText = "Added Word " + e.detail.name_input;
    successMessageOpen = true;
    setTimeout(() => {
      successMessageOpen = false;
    }, 1000);
  };
  const delete_a_book = (e) => {
    console.log(e.detail);
    notebooks = notebooks.filter((item) => {
      return item.id != e.detail.bookId;
    });
    console.log(notebooks);
    localStorage.setItem("chineseoo-notes", JSON.stringify(notebooks));
  };
  const delete_a_word = (e) => {
    console.log(e.detail);
    notebooks = notebooks.filter((item) => {
      item.data = item.data.filter((word) => {
        return word.id != e.detail.wordId;
      });
      console.log(item);
      return item;
    });
    console.log(notebooks);
    localStorage.setItem("chineseoo-notes", JSON.stringify(notebooks));
  };
  const move_one_word_up = (e) => {
    console.log(e.detail.itemIndex)
    let index1 = e.detail.itemIndex
    let index2 = e.detail.itemIndex - 1
    let bookId = e.detail.bookId
    notebooks = notebooks.filter((notebook) => {
      if (notebook.id == bookId){
        let temp = notebook.data[index1];
        notebook.data[index1] = notebook.data[index2]
        notebook.data[index2] = temp
      }
      return notebook
    })
    console.log(notebooks)
    localStorage.setItem("chineseoo-notes", JSON.stringify(notebooks));
  }
  routeChange();
</script>

<svelte:window on:hashchange={routeChange} />
<svelte:component
  this={page}
  bind:notebooks
  bind:hashParam
  on:chineseoo_add_new_book={add_new_book}
  on:chineseoo_add_new_word={add_new_word}
  on:chineseoo_delete_a_book={delete_a_book}
  on:chineseoo_delete_a_word={delete_a_word}
  on:chineseoo_move_one_word_up={move_one_word_up}
/>
{#if successMessageOpen}
  <SuccessToast messageText={successMessageText} />
{/if}
{#if errorMessageOpen}
  <ErrorToast messageText={errorMessageText} />
{/if}
