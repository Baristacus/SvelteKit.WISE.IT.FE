<script>
	import SqlEditor from '$lib/components/SQLEditor.svelte';

	let isCollapsed = false;
	let containerClass = 'container-fluid';

	function toggleCollapse() {
		isCollapsed = !isCollapsed;
		containerClass = isCollapsed ? 'container' : 'container-fluid';
	}
</script>

<svelte:head>
	<title>WISE IT: SQooL - 학습안내서</title>
	<meta name="description" content="WISE SQooL 학습안내서 페이지입니다." />
</svelte:head>

<div class={containerClass}>
	<div class="row">
		<div class={isCollapsed ? 'col-md-3' : 'col-md-2'}>
			<div class="card bg-light">
				<div class="card-body">
					<h5 class="card-title">시작하기</h5>
					<div class="card-text">
						<ul>
							<li>사전 체크 포인트</li>
							<li>환경설정</li>
						</ul>
					</div>
					<h5 class="card-title">SQL 학습안내</h5>
					<div class="card-text">
						<ul>
							<li>SQL 이란?</li>
							<li>테이블과 스키마</li>
							<li>데이터 출력</li>
						</ul>
					</div>
				</div>
			</div>
		</div>
		<div class={isCollapsed ? 'col-md-9' : 'col-md-4'}>
			<div class="d-grid">
				<button class="btn btn-info mb-3" on:click={toggleCollapse}>
					{isCollapsed ? 'SQL 에디터 펼치기' : 'SQL 에디터 접기'}
				</button>
			</div>
			<div class="card">
				<div class="card-body">
					<h4 class="card-title">시작하기</h4>
					<h6>사전 체크 포인트</h6>
					<p class="card-text">
						Some quick example text to build on the card title and make up the bulk of the card's
						content.
					</p>
					<h6>환경설정</h6>
					<p class="card-text">
						Some quick example text to build on the card title and make up the bulk of the card's
						content.
					</p>
				</div>
			</div>
		</div>
		{#if !isCollapsed}
			<div id="sqlEditor" class="col-md-6">
				<SqlEditor />
			</div>
		{/if}
	</div>
</div>

<style>
</style>
