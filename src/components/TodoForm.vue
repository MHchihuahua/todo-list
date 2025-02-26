<script setup>

</script>

<template>
    <form class="todo-form">
        <div class="delete-group">
            <button>
                <i class="fa-solid fa-trash"></i>
            </button>
        </div>

        <div class="form-group title-group">
            <label for="title">Title</label>
            <input type="text" id="title" placeholder="new item title">
        </div>

        <div class="form-group date-group">
            <label for="date">Date</label>
            <div class="date-container">
                <input type="date" id="date" placeholder="2022/05/17">
                <span>~</span>
                <input type="date" placeholder="2022/05/18">
            </div>
        </div>

        <div class="form-group image-group">
            <label for="image">Image</label>
            <div class="image-container">
                <button class="upload-button">Upload Image</button>
                <p class="divider">or</p>
                <input type="text" placeholder="請輸入圖片網址">
            </div>
        </div>

        <div class="form-group image-preview-group">
            <div class="image-preview">
                <img src="" alt="Preview">
            </div>
        </div>

        <div class="form-group content-group">
            <label for="content">Content</label>
            <div class="content-container">
                <textarea id="content" class="content-area" placeholder="content..."></textarea>
                <div class="char-count">0/200</div>
            </div>
        </div>
    </form>
</template>

<style scoped>
.todo-form {
    padding: 15px 25px;
    width: 100%;
    display: grid;
    gap: 16px;
    grid-template-columns: 1fr 1fr;
    grid-template-rows: 20px 100px 200px auto;
    grid-template-areas:
        ".  delete"
        "title date"
        "image image-preview"
        "content content";
}

.delete-group {
    grid-area: delete;
    display: flex;
    flex-direction: row;
    justify-content: flex-end;
}

.delete-group>button {
    background: none;
    border: none;
    font-size: 20px;
    cursor: pointer;
}

.title-group {
    grid-area: title;
}

.date-group {
    grid-area: date;
}

.image-group {
    grid-area: image;
}

.image-preview-group {
    grid-area: image-preview;
}

.content-group {
    grid-area: content;
}

.form-group {
    display: flex;
    flex-direction: column;
}

.date-container {
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.date-container>input {
    width: 48%;
}

.upload-button {
    width: 100%;
    height: 55px;
}

.image-container {
    display: flex;
    flex-direction: column;
    gap: 8px;
    align-items: center;
}

.image-preview {
    height: 150px;
    border: 1px solid #e0e0e0;
    border-radius: 10px;
    overflow: hidden;
    margin-top: 24px;
    background-color: #ebebeb;
}

.image-preview img {
    width: 100%;
    height: 100%;
    object-fit: cover;
}

.content-container {
    position: relative;
}

.content-area {
    width: 100%;
    height: 145px;
    resize: none;
}

.char-count {
    display: flex;
    justify-content: flex-end;
    padding-right: 15px;
    align-items: center;
    position: absolute;
    width: 115px;
    height: 45px;
    font-size: 14px;
    border-radius: 0 0 10px 0;
    background-color: #e7ffe9;
    bottom: 5px;
    right: 0;
}

.char-count::before {
    content: "";
    position: absolute;
    left: 0;
    top: 0;
    transform: translate(-50%, 0%);
    border-top: 45px solid #EBEBEB;
    border-bottom: 45px solid transparent;
    border-left: 45px solid transparent;
    border-right: 45px solid transparent;
}

input,
textarea {
    width: 100%;
}

@media (max-width: 768px) {
    .todo-form {
        grid-template-columns: 1fr;
        grid-template-rows: 20px 100px 100px 180px 180px auto;
        grid-template-areas:
            "delete"
            "title"
            "date"
            "image"
            "image-preview"
            "content";
    }
}
</style>
