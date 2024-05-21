<script lang="ts">
  import * as Card from '$lib/components/ui/card/index.js';
  import { DollarSign } from 'lucide-svelte';
  let name = 'Gustavo';
</script>

<h1 class="welcome mb-8">
  <span class="font-normal">Bem-vindo de volta, </span> {name}!
</h1>


<div class="grid gap-4 md:grid-cols-2 lg:grid-cols-4">
  <Card.Root>
    <Card.Header>
      <div class="flex flex-row items-center justify-between">
        <Card.Title>Saldo</Card.Title>
        <DollarSign size="24" />
      </div>
    </Card.Header>
    <Card.Content>hello</Card.Content>
  </Card.Root>
</div>