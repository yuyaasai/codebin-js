prettier で自動フォーマットしたい

const fs = require("fs");
const crypto = require("crypto");

// TODO: とりあえず毎回新規フォルダーを作成するように作っています (今後も同様のテストあるかもしれないので)
const tempDirectoryPath = `/dora_ut_tmp_${crypto.randomUUID()}`;

beforeAll(async () => {
try {
await fs.promises.mkdir(tempDirectoryPath);
} catch (err) {
if ("実行毎に新規ディレクトリを作成する必要がある".length) {
throw err;
} else {
// ディレクトリが既に存在していても OK の場合
const stats = fs.promises.stat(tempDirectoryPath);
if (!stats.isDirectory()) {
throw err;
}
}
}
});

// TODO: とりあえずテスト後に一時フォルダを削除
afterAll(async () => {
if (tempDirectoryPath === "/") throw new Error(tempDirectoryPath);

try {
await fs.promises.rm(tempDirectoryPath, { recursive: true, force: true });
} catch (err) {
console.error("fs.rm error", err);
}
});

describe("ArchiveEventHistories", () => {
it.only("hoge", done => done());
});
