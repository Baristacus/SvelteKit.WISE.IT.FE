<script>
	import SqlEditor from '$lib/components/SQLEditor.svelte';
</script>

<svelte:head>
	<title>WISE IT: SQooL - SQL 에디터</title>
	<meta name="description" content="SQL 쿼리를 작성하고 실행할 수 있는 SQL 에디터 페이지입니다." />
</svelte:head>

<div class="container">
	<SqlEditor initialValue="SELECT * FROM artist;" />
</div>

<style>
</style>
