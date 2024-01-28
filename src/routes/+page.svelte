<script lang="ts">
	import * as Tabs from '$lib/components/ui/tabs';
	import * as Card from '$lib/components/ui/card';
	import { Input } from '$lib/components/ui/input';
	import * as Table from '$lib/components/ui/table';
	import { writable } from 'svelte/store';
	import { SI } from '$lib/index';

	let SInotes = writable(new SI());

	$: $SInotes.IHM.MOY = $SInotes.IHM.TP * 0.2 + $SInotes.IHM.TD * 0.2 + $SInotes.IHM.EXAM * 0.6;
	$: $SInotes.GL.MOY = $SInotes.GL.TP * 0.2 + $SInotes.GL.TD * 0.2 + $SInotes.GL.EXAM * 0.6;
	$: $SInotes.COMPIL.MOY =
		$SInotes.COMPIL.TP * 0.2 + $SInotes.COMPIL.TD * 0.2 + $SInotes.COMPIL.EXAM * 0.6;
	$: $SInotes.SE.MOY = $SInotes.SE.TP * 0.2 + $SInotes.SE.TD * 0.2 + $SInotes.SE.EXAM * 0.6;
	$: $SInotes.PL.MOY = $SInotes.PL.TD * 0.4 + $SInotes.PL.EXAM * 0.6;
	$: $SInotes.PROBA.MOY = $SInotes.PROBA.TD * 0.4 + $SInotes.PROBA.EXAM * 0.6;
	$: $SInotes.ENVS.MOY = $SInotes.ENVS.EXAM;

	$: $SInotes.U1 = ($SInotes.IHM.MOY * 3 + $SInotes.GL.MOY * 3) / 6;
	$: $SInotes.U2 = ($SInotes.COMPIL.MOY * 3 + $SInotes.SE.MOY * 3) / 6;
	$: $SInotes.U3 = ($SInotes.PL.MOY * 2 + $SInotes.PROBA.MOY * 2) / 4;
	$: $SInotes.U4 = $SInotes.ENVS.MOY;

	$: $SInotes.MOY = ($SInotes.U1 * 6 + $SInotes.U2 * 6 + $SInotes.U3 * 4 + $SInotes.U4 * 1) / 17;
</script>

<div class="m-auto flex h-full items-center justify-center">
	<Tabs.Root value="SI" class="w-[500px]">
		<Tabs.List class="grid w-full grid-cols-2">
			<Tabs.Trigger value="SI">SI</Tabs.Trigger>
			<Tabs.Trigger value="ISIL">ISIL</Tabs.Trigger>
		</Tabs.List>
		<Tabs.Content value="SI">
			<Card.Root>
				<Card.Header>
					<Card.Title>SI</Card.Title>
				</Card.Header>
				<Card.Content class="space-y-2">
					<Table.Root>
						<Table.Header>
							<Table.Row>
								<Table.Head>Module</Table.Head>
								<Table.Head>TP</Table.Head>
								<Table.Head>TD</Table.Head>
								<Table.Head>EXAM</Table.Head>
								<Table.Head>Module Rate</Table.Head>
							</Table.Row>
						</Table.Header>
						<Table.Body>
							<!-- IHM -->
							<Table.Row>
								<Table.Cell>IHM</Table.Cell>
								<Table.Cell>
									<Input placeholder="TP" bind:value={$SInotes.IHM.TP} />
								</Table.Cell>
								<Table.Cell>
									<Input placeholder="TD" bind:value={$SInotes.IHM.TD} />
								</Table.Cell>
								<Table.Cell>
									<Input placeholder="EXAM" bind:value={$SInotes.IHM.EXAM} />
								</Table.Cell>
								<Table.Cell>
									<Input placeholder="MOY" disabled bind:value={$SInotes.IHM.MOY} />
								</Table.Cell>
							</Table.Row>

							<!-- GL -->
							<Table.Row>
								<Table.Cell>GL</Table.Cell>
								<Table.Cell>
									<Input placeholder="TP" bind:value={$SInotes.GL.TP} />
								</Table.Cell>
								<Table.Cell>
									<Input placeholder="TD" bind:value={$SInotes.GL.TD} />
								</Table.Cell>
								<Table.Cell>
									<Input placeholder="EXAM" bind:value={$SInotes.GL.EXAM} />
								</Table.Cell>
								<Table.Cell>
									<Input placeholder="MOY" disabled bind:value={$SInotes.GL.MOY} />
								</Table.Cell>
							</Table.Row>
							<!--U1-->
							<Table.Row>
								<Table.Cell>U1</Table.Cell>
								<Table.Cell colspan={4}>
									<Input placeholder="MOY" disabled bind:value={$SInotes.U1} />
								</Table.Cell>
							</Table.Row>
							<!-- SE -->
							<Table.Row>
								<Table.Cell>SE</Table.Cell>
								<Table.Cell>
									<Input placeholder="TP" bind:value={$SInotes.SE.TP} />
								</Table.Cell>
								<Table.Cell>
									<Input placeholder="TD" bind:value={$SInotes.SE.TD} />
								</Table.Cell>
								<Table.Cell>
									<Input placeholder="EXAM" bind:value={$SInotes.SE.EXAM} />
								</Table.Cell>
								<Table.Cell>
									<Input placeholder="MOY" disabled bind:value={$SInotes.SE.MOY} />
								</Table.Cell>
							</Table.Row>

							<!-- COMPIL -->
							<Table.Row>
								<Table.Cell>COMPIL</Table.Cell>
								<Table.Cell>
									<Input placeholder="TP" bind:value={$SInotes.COMPIL.TP} />
								</Table.Cell>
								<Table.Cell>
									<Input placeholder="TD" bind:value={$SInotes.COMPIL.TD} />
								</Table.Cell>
								<Table.Cell>
									<Input placeholder="EXAM" bind:value={$SInotes.COMPIL.EXAM} />
								</Table.Cell>
								<Table.Cell>
									<Input placeholder="MOY" disabled bind:value={$SInotes.COMPIL.MOY} />
								</Table.Cell>
							</Table.Row>
							<!--U2-->
							<Table.Row>
								<Table.Cell>U2</Table.Cell>
								<Table.Cell colspan={4}>
									<Input placeholder="MOY" disabled bind:value={$SInotes.U2} />
								</Table.Cell>
							</Table.Row>
							<!-- PL -->
							<Table.Row>
								<Table.Cell>PL</Table.Cell>
								<Table.Cell></Table.Cell>
								<Table.Cell>
									<Input placeholder="TD" bind:value={$SInotes.PL.TD} />
								</Table.Cell>
								<Table.Cell>
									<Input placeholder="EXAM" bind:value={$SInotes.PL.EXAM} />
								</Table.Cell>
								<Table.Cell>
									<Input placeholder="MOY" disabled bind:value={$SInotes.PL.MOY} />
								</Table.Cell>
							</Table.Row>

							<!-- PROBA -->
							<Table.Row>
								<Table.Cell>PROBA</Table.Cell>
								<Table.Cell></Table.Cell>
								<Table.Cell>
									<Input placeholder="TD" bind:value={$SInotes.PROBA.TD} />
								</Table.Cell>
								<Table.Cell>
									<Input placeholder="EXAM" bind:value={$SInotes.PROBA.EXAM} />
								</Table.Cell>
								<Table.Cell>
									<Input placeholder="MOY" disabled bind:value={$SInotes.PROBA.MOY} />
								</Table.Cell>
							</Table.Row>
							<!--U3-->
							<Table.Row>
								<Table.Cell>U3</Table.Cell>
								<Table.Cell colspan={4}>
									<Input placeholder="MOY" disabled bind:value={$SInotes.U3} />
								</Table.Cell>
							</Table.Row>
							<!-- ENVS -->
							<Table.Row>
								<Table.Cell>ENVS</Table.Cell>
								<Table.Cell></Table.Cell>
								<Table.Cell></Table.Cell>
								<Table.Cell>
									<Input placeholder="EXAM" bind:value={$SInotes.ENVS.EXAM} />
								</Table.Cell>
								<Table.Cell>
									<Input placeholder="MOY" disabled bind:value={$SInotes.ENVS.MOY} />
								</Table.Cell>
							</Table.Row>
							<!--U4-->
							<Table.Row>
								<Table.Cell>U4</Table.Cell>
								<Table.Cell colspan={4}>
									<Input placeholder="MOY" disabled bind:value={$SInotes.U4} />
								</Table.Cell>
							</Table.Row>
							<!--MOY-->
							<Table.Row>
								<Table.Cell>Mark</Table.Cell>
								<Table.Cell colspan={4}>
									<Input placeholder="MOY" disabled bind:value={$SInotes.MOY} />
								</Table.Cell>
							</Table.Row>
						</Table.Body>
					</Table.Root>
				</Card.Content>
			</Card.Root>
		</Tabs.Content>
		<Tabs.Content value="ISIL">
			<Card.Root>
				<Card.Header>
					<Card.Title>ISIL</Card.Title>
				</Card.Header>
				<Card.Content class="space-y-2">Not Available yet</Card.Content>
			</Card.Root>
		</Tabs.Content>
	</Tabs.Root>
</div>
