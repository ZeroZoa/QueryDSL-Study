<html><head><meta http-equiv="Content-Type" content="text/html; charset=utf-8"/><title>QueryDSL 핵심 정리 및 실무 활용 가이드</title><style>
/* cspell:disable-file */
/* webkit printing magic: print all background colors */
html {
	-webkit-print-color-adjust: exact;
}
* {
	box-sizing: border-box;
	-webkit-print-color-adjust: exact;
}

html,
body {
	margin: 0;
	padding: 0;
}
@media only screen {
	body {
		margin: 2em auto;
		max-width: 900px;
		color: rgb(55, 53, 47);
	}
}

body {
	line-height: 1.5;
	white-space: pre-wrap;
}

a,
a.visited {
	color: inherit;
	text-decoration: underline;
}

.pdf-relative-link-path {
	font-size: 80%;
	color: #444;
}

h1,
h2,
h3 {
	letter-spacing: -0.01em;
	line-height: 1.2;
	font-weight: 600;
	margin-bottom: 0;
}

.page-title {
	font-size: 2.5rem;
	font-weight: 700;
	margin-top: 0;
	margin-bottom: 0.75em;
}

h1 {
	font-size: 1.875rem;
	margin-top: 1.875rem;
}

h2 {
	font-size: 1.5rem;
	margin-top: 1.5rem;
}

h3 {
	font-size: 1.25rem;
	margin-top: 1.25rem;
}

.source {
	border: 1px solid #ddd;
	border-radius: 3px;
	padding: 1.5em;
	word-break: break-all;
}

.callout {
	border-radius: 10px;
	padding: 1rem;
}

figure {
	margin: 1.25em 0;
	page-break-inside: avoid;
}

figcaption {
	opacity: 0.5;
	font-size: 85%;
	margin-top: 0.5em;
}

mark {
	background-color: transparent;
}

.indented {
	padding-left: 1.5em;
}

hr {
	background: transparent;
	display: block;
	width: 100%;
	height: 1px;
	visibility: visible;
	border: none;
	border-bottom: 1px solid rgba(55, 53, 47, 0.09);
}

img {
	max-width: 100%;
}

@media only print {
	img {
		max-height: 100vh;
		object-fit: contain;
	}
}

@page {
	margin: 1in;
}

.collection-content {
	font-size: 0.875rem;
}

.collection-content td {
	white-space: pre-wrap;
	word-break: break-word;
}

.column-list {
	display: flex;
	justify-content: space-between;
}

.column {
	padding: 0 1em;
}

.column:first-child {
	padding-left: 0;
}

.column:last-child {
	padding-right: 0;
}

.table_of_contents-item {
	display: block;
	font-size: 0.875rem;
	line-height: 1.3;
	padding: 0.125rem;
}

.table_of_contents-indent-1 {
	margin-left: 1.5rem;
}

.table_of_contents-indent-2 {
	margin-left: 3rem;
}

.table_of_contents-indent-3 {
	margin-left: 4.5rem;
}

.table_of_contents-link {
	text-decoration: none;
	opacity: 0.7;
	border-bottom: 1px solid rgba(55, 53, 47, 0.18);
}

table,
th,
td {
	border: 1px solid rgba(55, 53, 47, 0.09);
	border-collapse: collapse;
}

table {
	border-left: none;
	border-right: none;
}

th,
td {
	font-weight: normal;
	padding: 0.25em 0.5em;
	line-height: 1.5;
	min-height: 1.5em;
	text-align: left;
}

th {
	color: rgba(55, 53, 47, 0.6);
}

ol,
ul {
	margin: 0;
	margin-block-start: 0.6em;
	margin-block-end: 0.6em;
}

li > ol:first-child,
li > ul:first-child {
	margin-block-start: 0.6em;
}

ul > li {
	list-style: disc;
}

ul.to-do-list {
	padding-inline-start: 0;
}

ul.to-do-list > li {
	list-style: none;
}

.to-do-children-checked {
	text-decoration: line-through;
	opacity: 0.375;
}

ul.toggle > li {
	list-style: none;
}

ul {
	padding-inline-start: 1.7em;
}

ul > li {
	padding-left: 0.1em;
}

ol {
	padding-inline-start: 1.6em;
}

ol > li {
	padding-left: 0.2em;
}

.mono ol {
	padding-inline-start: 2em;
}

.mono ol > li {
	text-indent: -0.4em;
}

.toggle {
	padding-inline-start: 0em;
	list-style-type: none;
}

/* Indent toggle children */
.toggle > li > details {
	padding-left: 1.7em;
}

.toggle > li > details > summary {
	margin-left: -1.1em;
}

.selected-value {
	display: inline-block;
	padding: 0 0.5em;
	background: rgba(206, 205, 202, 0.5);
	border-radius: 3px;
	margin-right: 0.5em;
	margin-top: 0.3em;
	margin-bottom: 0.3em;
	white-space: nowrap;
}

.collection-title {
	display: inline-block;
	margin-right: 1em;
}

.page-description {
	margin-bottom: 2em;
}

.simple-table {
	margin-top: 1em;
	font-size: 0.875rem;
	empty-cells: show;
}
.simple-table td {
	height: 29px;
	min-width: 120px;
}

.simple-table th {
	height: 29px;
	min-width: 120px;
}

.simple-table-header-color {
	background: rgb(247, 246, 243);
	color: black;
}
.simple-table-header {
	font-weight: 500;
}

time {
	opacity: 0.5;
}

.icon {
	display: inline-flex;
	align-items: center;
	justify-content: center;
	max-width: 1.2em;
	max-height: 1.2em;
	text-decoration: none;
	vertical-align: text-bottom;
	margin-right: 0.5em;
}

img.icon {
	border-radius: 3px;
}

.callout img.notion-static-icon {
	width: 1em;
	height: 1em;
}

.callout p {
	margin: 0;
}

.callout h1,
.callout h2,
.callout h3 {
	margin: 0 0 0.6rem;
}

.user-icon {
	width: 1.5em;
	height: 1.5em;
	border-radius: 100%;
	margin-right: 0.5rem;
}

.user-icon-inner {
	font-size: 0.8em;
}

.text-icon {
	border: 1px solid #000;
	text-align: center;
}

.page-cover-image {
	display: block;
	object-fit: cover;
	width: 100%;
	max-height: 30vh;
}

.page-header-icon {
	font-size: 3rem;
	margin-bottom: 1rem;
}

.page-header-icon-with-cover {
	margin-top: -0.72em;
	margin-left: 0.07em;
}

.page-header-icon img {
	border-radius: 3px;
}

.link-to-page {
	margin: 1em 0;
	padding: 0;
	border: none;
	font-weight: 500;
}

p > .user {
	opacity: 0.5;
}

td > .user,
td > time {
	white-space: nowrap;
}

input[type="checkbox"] {
	transform: scale(1.5);
	margin-right: 0.6em;
	vertical-align: middle;
}

p {
	margin-top: 0.5em;
	margin-bottom: 0.5em;
}

.image {
	border: none;
	margin: 1.5em 0;
	padding: 0;
	border-radius: 0;
	text-align: center;
}

.code,
code {
	background: rgba(135, 131, 120, 0.15);
	border-radius: 3px;
	padding: 0.2em 0.4em;
	border-radius: 3px;
	font-size: 85%;
	tab-size: 2;
}

code {
	color: #eb5757;
}

.code {
	padding: 1.5em 1em;
}

.code-wrap {
	white-space: pre-wrap;
	word-break: break-all;
}

.code > code {
	background: none;
	padding: 0;
	font-size: 100%;
	color: inherit;
}

blockquote {
	font-size: 1em;
	margin: 1em 0;
	padding-left: 1em;
	border-left: 3px solid rgb(55, 53, 47);
}

blockquote.quote-large {
	font-size: 1.25em;
}

.bookmark {
	text-decoration: none;
	max-height: 8em;
	padding: 0;
	display: flex;
	width: 100%;
	align-items: stretch;
}

.bookmark-title {
	font-size: 0.85em;
	overflow: hidden;
	text-overflow: ellipsis;
	height: 1.75em;
	white-space: nowrap;
}

.bookmark-text {
	display: flex;
	flex-direction: column;
}

.bookmark-info {
	flex: 4 1 180px;
	padding: 12px 14px 14px;
	display: flex;
	flex-direction: column;
	justify-content: space-between;
}

.bookmark-image {
	width: 33%;
	flex: 1 1 180px;
	display: block;
	position: relative;
	object-fit: cover;
	border-radius: 1px;
}

.bookmark-description {
	color: rgba(55, 53, 47, 0.6);
	font-size: 0.75em;
	overflow: hidden;
	max-height: 4.5em;
	word-break: break-word;
}

.bookmark-href {
	font-size: 0.75em;
	margin-top: 0.25em;
}

.sans { font-family: ui-sans-serif, -apple-system, BlinkMacSystemFont, "Segoe UI Variable Display", "Segoe UI", Helvetica, "Apple Color Emoji", Arial, sans-serif, "Segoe UI Emoji", "Segoe UI Symbol"; }
.code { font-family: "SFMono-Regular", Menlo, Consolas, "PT Mono", "Liberation Mono", Courier, monospace; }
.serif { font-family: Lyon-Text, Georgia, ui-serif, serif; }
.mono { font-family: iawriter-mono, Nitti, Menlo, Courier, monospace; }
.pdf .sans { font-family: Inter, ui-sans-serif, -apple-system, BlinkMacSystemFont, "Segoe UI Variable Display", "Segoe UI", Helvetica, "Apple Color Emoji", Arial, sans-serif, "Segoe UI Emoji", "Segoe UI Symbol", 'Twemoji', 'Noto Color Emoji', 'Noto Sans CJK JP'; }
.pdf:lang(zh-CN) .sans { font-family: Inter, ui-sans-serif, -apple-system, BlinkMacSystemFont, "Segoe UI Variable Display", "Segoe UI", Helvetica, "Apple Color Emoji", Arial, sans-serif, "Segoe UI Emoji", "Segoe UI Symbol", 'Twemoji', 'Noto Color Emoji', 'Noto Sans CJK SC'; }
.pdf:lang(zh-TW) .sans { font-family: Inter, ui-sans-serif, -apple-system, BlinkMacSystemFont, "Segoe UI Variable Display", "Segoe UI", Helvetica, "Apple Color Emoji", Arial, sans-serif, "Segoe UI Emoji", "Segoe UI Symbol", 'Twemoji', 'Noto Color Emoji', 'Noto Sans CJK TC'; }
.pdf:lang(ko-KR) .sans { font-family: Inter, ui-sans-serif, -apple-system, BlinkMacSystemFont, "Segoe UI Variable Display", "Segoe UI", Helvetica, "Apple Color Emoji", Arial, sans-serif, "Segoe UI Emoji", "Segoe UI Symbol", 'Twemoji', 'Noto Color Emoji', 'Noto Sans CJK KR'; }
.pdf .code { font-family: Source Code Pro, "SFMono-Regular", Menlo, Consolas, "PT Mono", "Liberation Mono", Courier, monospace, 'Twemoji', 'Noto Color Emoji', 'Noto Sans Mono CJK JP'; }
.pdf:lang(zh-CN) .code { font-family: Source Code Pro, "SFMono-Regular", Menlo, Consolas, "PT Mono", "Liberation Mono", Courier, monospace, 'Twemoji', 'Noto Color Emoji', 'Noto Sans Mono CJK SC'; }
.pdf:lang(zh-TW) .code { font-family: Source Code Pro, "SFMono-Regular", Menlo, Consolas, "PT Mono", "Liberation Mono", Courier, monospace, 'Twemoji', 'Noto Color Emoji', 'Noto Sans Mono CJK TC'; }
.pdf:lang(ko-KR) .code { font-family: Source Code Pro, "SFMono-Regular", Menlo, Consolas, "PT Mono", "Liberation Mono", Courier, monospace, 'Twemoji', 'Noto Color Emoji', 'Noto Sans Mono CJK KR'; }
.pdf .serif { font-family: PT Serif, Lyon-Text, Georgia, ui-serif, serif, 'Twemoji', 'Noto Color Emoji', 'Noto Serif CJK JP'; }
.pdf:lang(zh-CN) .serif { font-family: PT Serif, Lyon-Text, Georgia, ui-serif, serif, 'Twemoji', 'Noto Color Emoji', 'Noto Serif CJK SC'; }
.pdf:lang(zh-TW) .serif { font-family: PT Serif, Lyon-Text, Georgia, ui-serif, serif, 'Twemoji', 'Noto Color Emoji', 'Noto Serif CJK TC'; }
.pdf:lang(ko-KR) .serif { font-family: PT Serif, Lyon-Text, Georgia, ui-serif, serif, 'Twemoji', 'Noto Color Emoji', 'Noto Serif CJK KR'; }
.pdf .mono { font-family: PT Mono, iawriter-mono, Nitti, Menlo, Courier, monospace, 'Twemoji', 'Noto Color Emoji', 'Noto Sans Mono CJK JP'; }
.pdf:lang(zh-CN) .mono { font-family: PT Mono, iawriter-mono, Nitti, Menlo, Courier, monospace, 'Twemoji', 'Noto Color Emoji', 'Noto Sans Mono CJK SC'; }
.pdf:lang(zh-TW) .mono { font-family: PT Mono, iawriter-mono, Nitti, Menlo, Courier, monospace, 'Twemoji', 'Noto Color Emoji', 'Noto Sans Mono CJK TC'; }
.pdf:lang(ko-KR) .mono { font-family: PT Mono, iawriter-mono, Nitti, Menlo, Courier, monospace, 'Twemoji', 'Noto Color Emoji', 'Noto Sans Mono CJK KR'; }
.highlight-default {
	color: rgba(44, 44, 43, 1);
}
.highlight-gray {
	color: rgba(125, 122, 117, 1);
	fill: rgba(125, 122, 117, 1);
}
.highlight-brown {
	color: rgba(159, 118, 90, 1);
	fill: rgba(159, 118, 90, 1);
}
.highlight-orange {
	color: rgba(210, 123, 45, 1);
	fill: rgba(210, 123, 45, 1);
}
.highlight-yellow {
	color: rgba(203, 148, 52, 1);
	fill: rgba(203, 148, 52, 1);
}
.highlight-teal {
	color: rgba(80, 148, 110, 1);
	fill: rgba(80, 148, 110, 1);
}
.highlight-blue {
	color: rgba(56, 125, 201, 1);
	fill: rgba(56, 125, 201, 1);
}
.highlight-purple {
	color: rgba(154, 107, 180, 1);
	fill: rgba(154, 107, 180, 1);
}
.highlight-pink {
	color: rgba(193, 76, 138, 1);
	fill: rgba(193, 76, 138, 1);
}
.highlight-red {
	color: rgba(207, 81, 72, 1);
	fill: rgba(207, 81, 72, 1);
}
.highlight-default_background {
	color: rgba(44, 44, 43, 1);
}
.highlight-gray_background {
	background: rgba(42, 28, 0, 0.07);
}
.highlight-brown_background {
	background: rgba(139, 46, 0, 0.086);
}
.highlight-orange_background {
	background: rgba(224, 101, 1, 0.129);
}
.highlight-yellow_background {
	background: rgba(211, 168, 0, 0.137);
}
.highlight-teal_background {
	background: rgba(0, 100, 45, 0.09);
}
.highlight-blue_background {
	background: rgba(0, 124, 215, 0.094);
}
.highlight-purple_background {
	background: rgba(102, 0, 178, 0.078);
}
.highlight-pink_background {
	background: rgba(197, 0, 93, 0.086);
}
.highlight-red_background {
	background: rgba(223, 22, 0, 0.094);
}
.block-color-default {
	color: inherit;
	fill: inherit;
}
.block-color-gray {
	color: rgba(125, 122, 117, 1);
	fill: rgba(125, 122, 117, 1);
}
.block-color-brown {
	color: rgba(159, 118, 90, 1);
	fill: rgba(159, 118, 90, 1);
}
.block-color-orange {
	color: rgba(210, 123, 45, 1);
	fill: rgba(210, 123, 45, 1);
}
.block-color-yellow {
	color: rgba(203, 148, 52, 1);
	fill: rgba(203, 148, 52, 1);
}
.block-color-teal {
	color: rgba(80, 148, 110, 1);
	fill: rgba(80, 148, 110, 1);
}
.block-color-blue {
	color: rgba(56, 125, 201, 1);
	fill: rgba(56, 125, 201, 1);
}
.block-color-purple {
	color: rgba(154, 107, 180, 1);
	fill: rgba(154, 107, 180, 1);
}
.block-color-pink {
	color: rgba(193, 76, 138, 1);
	fill: rgba(193, 76, 138, 1);
}
.block-color-red {
	color: rgba(207, 81, 72, 1);
	fill: rgba(207, 81, 72, 1);
}
.block-color-default_background {
	color: inherit;
	fill: inherit;
}
.block-color-gray_background {
	background: rgba(240, 239, 237, 1);
}
.block-color-brown_background {
	background: rgba(245, 237, 233, 1);
}
.block-color-orange_background {
	background: rgba(251, 235, 222, 1);
}
.block-color-yellow_background {
	background: rgba(249, 243, 220, 1);
}
.block-color-teal_background {
	background: rgba(232, 241, 236, 1);
}
.block-color-blue_background {
	background: rgba(229, 242, 252, 1);
}
.block-color-purple_background {
	background: rgba(243, 235, 249, 1);
}
.block-color-pink_background {
	background: rgba(250, 233, 241, 1);
}
.block-color-red_background {
	background: rgba(252, 233, 231, 1);
}
.select-value-color-default { background-color: rgba(42, 28, 0, 0.07); }
.select-value-color-gray { background-color: rgba(28, 19, 1, 0.11); }
.select-value-color-brown { background-color: rgba(127, 51, 0, 0.156); }
.select-value-color-orange { background-color: rgba(196, 88, 0, 0.203); }
.select-value-color-yellow { background-color: rgba(209, 156, 0, 0.282); }
.select-value-color-green { background-color: rgba(0, 96, 38, 0.156); }
.select-value-color-blue { background-color: rgba(0, 118, 217, 0.203); }
.select-value-color-purple { background-color: rgba(92, 0, 163, 0.141); }
.select-value-color-pink { background-color: rgba(183, 0, 78, 0.152); }
.select-value-color-red { background-color: rgba(206, 24, 0, 0.164); }

.checkbox {
	display: inline-flex;
	vertical-align: text-bottom;
	width: 16;
	height: 16;
	background-size: 16px;
	margin-left: 2px;
	margin-right: 5px;
}

.checkbox-on {
	background-image: url("data:image/svg+xml;charset=UTF-8,%3Csvg%20width%3D%2216%22%20height%3D%2216%22%20viewBox%3D%220%200%2016%2016%22%20fill%3D%22none%22%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%3E%0A%3Crect%20width%3D%2216%22%20height%3D%2216%22%20fill%3D%22%2358A9D7%22%2F%3E%0A%3Cpath%20d%3D%22M6.71429%2012.2852L14%204.9995L12.7143%203.71436L6.71429%209.71378L3.28571%206.2831L2%207.57092L6.71429%2012.2852Z%22%20fill%3D%22white%22%2F%3E%0A%3C%2Fsvg%3E");
}

.checkbox-off {
	background-image: url("data:image/svg+xml;charset=UTF-8,%3Csvg%20width%3D%2216%22%20height%3D%2216%22%20viewBox%3D%220%200%2016%2016%22%20fill%3D%22none%22%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%3E%0A%3Crect%20x%3D%220.75%22%20y%3D%220.75%22%20width%3D%2214.5%22%20height%3D%2214.5%22%20fill%3D%22white%22%20stroke%3D%22%2336352F%22%20stroke-width%3D%221.5%22%2F%3E%0A%3C%2Fsvg%3E");
}
	
</style></head><body><article id="2b9366ef-a824-808f-9773-f5150343ef83" class="page sans"><header><h1 class="page-title">QueryDSL 핵심 정리 및 실무 활용 가이드</h1><p class="page-description"></p></header><div class="page-body"><h2 id="2b9366ef-a824-80c8-8b75-de1a88da28cb" class="">1. QueryDSL이란?</h2><p id="2b9366ef-a824-80b4-a95f-d5bb8ed17f15" class=""><strong>QueryDSL</strong>은 하이버네이트 쿼리 언어(HQL) 또는 **JPQL(Java Persistence Query Language)**을 문자열이 아닌 <strong>자바 코드</strong>로 작성할 수 있도록 도와주는 오픈소스 빌더 프레임워크입니다.</p><h3 id="2b9366ef-a824-8051-8ca2-f70a4d6b84c9" class="">왜 사용하는가?</h3><ul id="2b9366ef-a824-80a3-ad8d-dd2cd54c9f85" class="bulleted-list"><li style="list-style-type:disc">기본적인 CRUD는 <code>Spring Data JPA</code>로 해결 가능하지만, 복잡한 조회 쿼리나 동적 쿼리를 구현하기에는 한계가 있습니다.</li></ul><ul id="2b9366ef-a824-8078-92de-c6492a2f8723" class="bulleted-list"><li style="list-style-type:disc">문자열(String) 형태의 JPQL은 런타임 시점에 오류가 발견되지만, QueryDSL은 코드 기반이므로 <strong>컴파일 시점에 문법 오류를 잡을 수 있습니다.</strong></li></ul><hr id="2b9366ef-a824-80de-ab1c-f5c5fbe84e81"/><h2 id="2b9366ef-a824-809f-8014-d40421e37a97" class="">2. 주요 특징 및 장점</h2><ol type="1" id="2b9366ef-a824-8057-93f7-e1d495dcd562" class="numbered-list" start="1"><li><strong>타입 안전성 (Type Safety)</strong><ul id="2b9366ef-a824-80e8-a1f7-debc0bae2adb" class="bulleted-list"><li style="list-style-type:disc"><code>QEntity</code>라는 전용 클래스를 사용하여 코드로 작성하므로, 오타나 존재하지 않는 필드 참조 시 컴파일 에러가 발생하여 안전합니다.</li></ul></li></ol><ol type="1" id="2b9366ef-a824-80f8-886d-fae74d0779a1" class="numbered-list" start="2"><li><strong>동적 쿼리 해결 (Dynamic Query)</strong><ul id="2b9366ef-a824-80c6-b943-ca121a962c23" class="bulleted-list"><li style="list-style-type:disc"><code>BooleanExpression</code>을 활용하여 조건문을 메서드 단위로 분리하고 조합할 수 있습니다.</li></ul><ul id="2b9366ef-a824-80fc-9d36-e5b770e79573" class="bulleted-list"><li style="list-style-type:disc">조건이 <code>null</code>일 경우 <code>Where</code> 절에서 자동으로 무시되므로 동적 쿼리 작성이 매우 유연합니다.</li></ul></li></ol><ol type="1" id="2b9366ef-a824-802b-b49b-df3820c6f9e0" class="numbered-list" start="3"><li><strong>가독성 및 유지보수</strong><ul id="2b9366ef-a824-80e8-95c5-d6c8bc3b8d4e" class="bulleted-list"><li style="list-style-type:disc">SQL과 유사한 직관적인 문법을 제공합니다.</li></ul><ul id="2b9366ef-a824-8029-9e29-ef9ebf91ebf4" class="bulleted-list"><li style="list-style-type:disc">복잡한 쿼리 로직을 메서드로 분리하여 재사용할 수 있습니다.</li></ul></li></ol><hr id="2b9366ef-a824-80a6-a0f8-d13cbffdfbd0"/><h2 id="2b9366ef-a824-808d-b7e8-d2bad8917b41" class="">3. 기본 문법</h2><h3 id="2b9366ef-a824-8004-92c6-e83fa97187c2" class="">검색 조건 (Where 절)</h3><ul id="2b9366ef-a824-80c9-8d2e-f672825bea72" class="bulleted-list"><li style="list-style-type:disc"><strong>비교:</strong> <code>.eq()</code>, <code>.ne()</code>, <code>.gt()</code>, <code>.lt()</code>, <code>.goe()</code>, <code>.loe()</code></li></ul><ul id="2b9366ef-a824-800d-8565-e16cfcd8afbb" class="bulleted-list"><li style="list-style-type:disc"><strong>범위:</strong> <code>.between()</code>, <code>.in()</code>, <code>.notIn()</code></li></ul><ul id="2b9366ef-a824-80f0-a7dc-c34b83b96163" class="bulleted-list"><li style="list-style-type:disc"><strong>검색:</strong> <code>.like()</code>, <code>.contains()</code>, <code>.startsWith()</code>, <code>.endsWith()</code></li></ul><ul id="2b9366ef-a824-80d0-8d09-e71c052d2bc9" class="bulleted-list"><li style="list-style-type:disc"><strong>논리 연산:</strong> <code>.and()</code>, <code>.or()</code>, <code>.not()</code></li></ul><h3 id="2b9366ef-a824-80ad-bc07-e4cc815bfc51" class="">정렬 및 조회 (OrderBy, Fetch)</h3><ul id="2b9366ef-a824-802f-902c-d9aef913b57b" class="bulleted-list"><li style="list-style-type:disc"><code>.orderBy(e.field.desc())</code>: 내림차순 정렬 (<code>asc()</code>: 오름차순)</li></ul><ul id="2b9366ef-a824-80f0-a595-c89a0f478f56" class="bulleted-list"><li style="list-style-type:disc"><code>.nullsLast()</code>, <code>.nullsFirst()</code>: null 값의 정렬 순서 지정</li></ul><ul id="2b9366ef-a824-806a-a3e9-f28489e7b1f6" class="bulleted-list"><li style="list-style-type:disc"><code>.fetch()</code>: 리스트 반환</li></ul><ul id="2b9366ef-a824-8049-8085-d98f94fabb1a" class="bulleted-list"><li style="list-style-type:disc"><code>.fetchOne()</code>: 단건 조회 (결과 없으면 null, 둘 이상이면 예외 발생)</li></ul><ul id="2b9366ef-a824-80e3-b170-ef8539a9627b" class="bulleted-list"><li style="list-style-type:disc"><code>.fetchFirst()</code>: <code>.limit(1).fetchOne()</code>과 동일</li></ul><hr id="2b9366ef-a824-8040-a9a1-e7123feec50d"/><h2 id="2b9366ef-a824-802b-98f0-e225192b2fed" class="">4. 실무 활용 전략 (Best Practices)</h2><h3 id="2b9366ef-a824-8061-b646-f522d201abaf" class="">1) 페이징(Paging) 성능 최적화</h3><ul id="2b9366ef-a824-8061-a8bf-c1b0307c0713" class="bulleted-list"><li style="list-style-type:disc"><code>fetchResults()</code>와 <code>fetchCount()</code>는 QueryDSL 5.0부터 <strong>Deprecated</strong> 되었습니다.</li></ul><ul id="2b9366ef-a824-80cc-bdfe-dd7c558770db" class="bulleted-list"><li style="list-style-type:disc">따라서 Content 쿼리와 Count 쿼리를 별도로 작성하여 분리하는 것이 권장됩니다.</li></ul><ul id="2b9366ef-a824-8024-8efe-dd028220b7c7" class="bulleted-list"><li style="list-style-type:disc">특히 Count 쿼리에서는 데이터 조회에 불필요한 <code>Join</code>을 제거하거나 최적화하여 성능을 높여야 합니다.</li></ul><h3 id="2b9366ef-a824-803f-8224-c39c751c34f5" class="">2) DTO 직접 조회 (Projections)</h3><ul id="2b9366ef-a824-8053-96f2-d32124f6fb8b" class="bulleted-list"><li style="list-style-type:disc">엔티티를 직접 조회하여 컨트롤러까지 넘기기보다는, 필요한 데이터만 뽑아 DTO로 반환하는 방식을 선호합니다.</li></ul><ul id="2b9366ef-a824-8077-b928-fa92a85e35a2" class="bulleted-list"><li style="list-style-type:disc"><code><strong>Projections.constructor</strong></code> 방식을 사용하여 생성자 기반으로 바인딩하면, 필드명 불일치 문제를 피하고 불변 객체로 활용할 수 있습니다. (단, 생성자 파라미터 순서와 타입이 일치해야 함)</li></ul><h3 id="2b9366ef-a824-80b3-9672-d6cd6015c98b" class="">3) BooleanExpression을 활용한 조건 모듈화</h3><ul id="2b9366ef-a824-80e8-9198-c60173a9357b" class="bulleted-list"><li style="list-style-type:disc"><code>where</code> 절에 들어갈 조건을 별도의 메서드(<code>BooleanExpression</code> 반환)로 분리합니다.</li></ul><ul id="2b9366ef-a824-80f2-b497-ededa8ae84ed" class="bulleted-list"><li style="list-style-type:disc">이렇게 하면 코드 가독성이 좋아지고, <code>isServiceable()</code> 같은 비즈니스 용어의 메서드로 만들어 다른 조회 로직에서도 재사용할 수 있습니다.</li></ul><h3 id="2b9366ef-a824-801b-ac19-f989f0cd91f3" class="">4) N+1 문제 해결 (Fetch Join)</h3><ul id="2b9366ef-a824-8090-9a6b-f015a27826e1" class="bulleted-list"><li style="list-style-type:disc">연관된 엔티티를 한 번에 가져올 때 <code>.fetchJoin()</code>을 사용합니다.</li></ul><ul id="2b9366ef-a824-800e-b897-effbe97c1799" class="bulleted-list"><li style="list-style-type:disc"><strong>주의:</strong> 컬렉션(1:N) 페치 조인 시 페이징을 하면 하이버네이트가 메모리에서 페이징 처리를 하므로 장애 원인이 될 수 있습니다. (N:1 관계는 안전)</li></ul><h3 id="2b9366ef-a824-808e-b3df-ef9db13065b0" class="">5) 영속성 컨텍스트 주의 (Bulk 연산)</h3><ul id="2b9366ef-a824-80d6-9892-cecfe758d374" class="bulleted-list"><li style="list-style-type:disc"><code>update</code>, <code>delete</code> 같은 벌크 연산은 영속성 컨텍스트(1차 캐시)를 무시하고 DB에 바로 반영됩니다.</li></ul><ul id="2b9366ef-a824-8030-abf4-c9dbef33242b" class="bulleted-list"><li style="list-style-type:disc">데이터 불일치를 막기 위해 벌크 연산 실행 후에는 반드시 <code>em.flush()</code>와 <code>em.clear()</code>를 호출해야 합니다.</li></ul><hr id="2b9366ef-a824-80dc-93d9-f052eb16f026"/><h2 id="2b9366ef-a824-80ad-8ee5-e114cf611ba1" class="">5. 코드 예제</h2><p id="2b9366ef-a824-80cf-9cbc-c11aa38c45dd" class="">아래는 동적 쿼리, DTO 매핑, 서브쿼리, 조인을 활용한 예제입니다.</p><script src="https://cdnjs.cloudflare.com/ajax/libs/prism/1.29.0/prism.min.js" integrity="sha512-7Z9J3l1+EYfeaPKcGXu3MS/7T+w19WtKQY/n+xzmw4hZhJ9tyYmcUS+4QqAlzhicE5LAfMQSF3iFTK9bQdTxXg==" crossorigin="anonymous" referrerPolicy="no-referrer"></script><link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/prism/1.29.0/themes/prism.min.css" integrity="sha512-tN7Ec6zAFaVSG3TpNAKtk4DOHNpSwKHxxrsiw4GHKESGPs5njn/0sMCUMl2svV4wo4BK/rCP7juYz+zx+l6oeQ==" crossorigin="anonymous" referrerPolicy="no-referrer"/><pre id="2b9366ef-a824-80e3-a099-feacd16a9f3e" class="code code-wrap"><code class="language-Java" style="white-space:pre-wrap;word-break:break-all">QEntity e = QEntity.entity

List&lt;Entity&gt; list = queryFactory
    .selectFrom(e) //e 테이블 선택
    .where(
        e.name.eq(&quot;aaa&quot;), //name이 aaa이면서
        e.size.gt(180) //size가 180보다 큰
    )
    .orderBy(e.createdAt.desc()) // createdAt을 기준으로 내림차순
    .fetch(); //query실행후 List 반환

</code></pre><script src="https://cdnjs.cloudflare.com/ajax/libs/prism/1.29.0/prism.min.js" integrity="sha512-7Z9J3l1+EYfeaPKcGXu3MS/7T+w19WtKQY/n+xzmw4hZhJ9tyYmcUS+4QqAlzhicE5LAfMQSF3iFTK9bQdTxXg==" crossorigin="anonymous" referrerPolicy="no-referrer"></script><link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/prism/1.29.0/themes/prism.min.css" integrity="sha512-tN7Ec6zAFaVSG3TpNAKtk4DOHNpSwKHxxrsiw4GHKESGPs5njn/0sMCUMl2svV4wo4BK/rCP7juYz+zx+l6oeQ==" crossorigin="anonymous" referrerPolicy="no-referrer"/><pre id="2b9366ef-a824-80e0-8eb8-e51a9c12c76f" class="code code-wrap"><code class="language-Java" style="white-space:pre-wrap;word-break:break-all">public List&lt;MemberDto&gt; searchMembers(String username, Integer minAge, Integer maxAge, String teamName) {
    QMember m = QMember.member; // Member 엔티티를 기반으로 자동 생성된 Q타입
    QTeam t = QTeam.team; // Team엔티티를 기반으로 자동 생성된 Q타입
    QMember sub = new QMember(&quot;sub&quot;); // 서브쿼리용 별칭

    return queryFactory
        .select(Projections.constructor(MemberDto.class, //원하는 결과값만 프로잭션
            m.id,
            m.username,
            t.name))
        .from(m) //Member 엔티티를 기준으로 조회
        .leftJoin(m.team, t) //Member와 Team을 join(팀이 없는 회원도 포함)
        .where(
            // null 무시 패턴: 값이 없으면 조건 제외
            usernameEq(username),
            ageGoe(minAge),
            ageLoe(maxAge),
            teamNameEq(teamName),

            // 서브쿼리: 평균 나이보다 많은 회원만
            m.age.gt(
                JPAExpressions // JPA환경에서 서브쿼리 작성을 위함
                    .select(sub.age.avg())
                    .from(sub)
            )
        )
        // 최신 가입일 기준 내림차순 정렬
        .orderBy(m.createdAt.desc())
        .fetch(); //fetch말고도 fetchOne(), fetchFirst(), fetchCount()등의 값도 있음
}

// 조건 생성기 (BooleanExpression 반환, null이면 where절에서 무시됨)
이이
private BooleanExpression ageGoe(Integer minAge) {
    return minAge != null ? QMember.member.age.goe(minAge) : null;
}
private BooleanExpression ageLoe(Integer maxAge) {
    return maxAge != null ? QMember.member.age.loe(maxAge) : null;
}
private BooleanExpression teamNameEq(String teamName) {
    return (teamName != null &amp;&amp; !teamName.isBlank()) ? QTeam.team.name.eq(teamName) : null;
}</code></pre><p id="2b9366ef-a824-802e-ad5a-f2b5bab0d41f" class="">
</p><p id="2b9366ef-a824-8013-a04e-ed87c0b002e5" class="">
</p></div></article><span class="sans" style="font-size:14px;padding-top:2em"></span></body></html>
